---
title: "Phase 4-A — 音声生成（VOICEVOX）"
---

## このチャプターで学ぶこと

- VOICEVOX Engine の API 構成（`audio_query` → `synthesis`）
- 発音辞書の仕組み（`pronunciation-dictionary.json`）
- イントネーション改善テクニック（読点配置、intonationScale、pitchScale）
- 感情別パラメータ設定マトリクス
- `audio-pipeline` の自動実行フロー
- 品質ゲート（尺チェック: 8〜20 分）
- Git LFS 問題の抜本対策

---

## 背景 — 合成音声の品質が動画の印象を決める

テック解説チャンネルの動画では、視聴者が最初に感じるのは **音声の自然さ** です。どれだけ内容が良くても、音声が不自然だと「ロボットが読み上げているだけ」という印象になり、視聴離脱につながります。

VOICEVOX は高品質な日本語音声合成エンジンですが、デフォルトのままでは以下の問題があります。

- **英語用語の誤読**: 「Claude Code」が「クラウデ コデ」と読まれる
- **漢字の誤読**: 「数百」が「かずひゃく」（正しくは「すうひゃく」）と読まれる
- **長文のイントネーション平坦化**: 60 文字超の文でピッチ変化が失われる
- **疑問文の語尾**: `？` を付けていないと疑問文なのに語尾が下がる

本プロジェクトでは、これらを **発音辞書 + テキスト前処理 + パラメータ最適化** の 3 層で解決しています。

---

## 設計思想

### VOICEVOX Engine の API フロー

VOICEVOX Engine は REST API で動作します。音声生成は 2 ステップの API 呼び出しで行います。

```
Step 1: POST /audio_query?text={テキスト}&speaker={speaker_id}
  → AudioQuery JSON（アクセント情報・モーラ情報を含む）

Step 2: POST /synthesis?speaker={speaker_id}
  → Body: AudioQuery JSON
  → Response: WAV バイナリ
```

`audio_query` が返す JSON には `accent_phrases` 配列が含まれ、各アクセント句のモーラ（音素）ごとにピッチ値が設定されています。このピッチ値を操作することで、イントネーションを制御できます。

### 3 層の音声品質改善

```
Layer 1: 発音辞書（pronunciation-dictionary.json）
  英語用語→カタカナ、難読語→ひらがなに置換
  ↓
Layer 2: 日本語読み補正（apply_japanese_reading_rules）
  「数+助数詞」「何+助数詞」等の正規表現ベース補正
  ↓
Layer 3: テキスト前処理 + パラメータ最適化
  カギ括弧除去、読点補完、感情別パラメータ適用
```

---

## 実装詳細

### 発音辞書の仕組み

`docs/pronunciation-dictionary.json` に英語用語・難読語のカタカナ / ひらがな読みを管理しています。

```json
{
  "_comment": "VOICEVOX音声生成用の発音辞書。...",
  "_verified_ok": "VOICEVOX実機テストで正常と確認済みの用語（長母音mora差は誤検知）: 三つ巴、審美眼",
  "terms": [
    {
      "pattern": "Claude Code",
      "reading": "クロード コード",
      "category": "製品名",
      "english": "Claude Code"
    },
    {
      "pattern": "Anthropic",
      "reading": "アンスロピック",
      "category": "企業名",
      "english": "Anthropic"
    },
    {
      "pattern": "深掘り",
      "reading": "ふかぼり",
      "category": "日本語難読"
    }
  ]
}
```

`generate_audio.py` は辞書のパターンを **長い順にソート** して適用します。これにより「Reinforcement Learning from Human Feedback」のような長いパターンが「Reinforcement」単体より先にマッチします。

```python
import re

def apply_pronunciation(text: str, terms: list) -> str:
    """英語用語・難読語をカタカナ/ひらがな読みに置換（大文字小文字を区別しない）"""
    for term in terms:
        text = re.sub(re.escape(term["pattern"]), term["reading"], text, flags=re.IGNORECASE)
    return text
```

:::message
**元テキストは保持する**: 発音テキストは音声生成にのみ使用します。タイムド台本（`*_timed.json`）の `text` フィールドには元のテキストを保持し、字幕表示には元テキストを使います。
:::

### 日本語読み補正（正規表現ベース）

発音辞書では網羅しきれない体系的な誤読パターンを、正規表現で補正します。`generate_audio.py` の `apply_japanese_reading_rules()` 関数が担当します。

代表的なパターンを紹介します。

**「数」+ 助数詞パターン**（最頻出）:

VOICEVOX の形態素解析（MeCab）が「数」を名詞「かず」として解析し、接頭辞「すう」と読むべき箇所で誤読します。

```python
# 「数百」→「すうひゃく」、「数千」→「すうせん」等
_RE_SUU_COUNTER = re.compile(r'数([十百千万億兆]+)')
```

**「何」+ 助数詞パターン**:

```python
# 「何百」→「なんびゃく」、「何人」→「なんにん」等
_RE_NAN_COUNTER = re.compile(
    r'何([百千万億兆十個人件回年月日時分秒度倍杯本枚台])'
)
```

**「行」の読み分け**:

```python
# 「行う」→「おこなう」、「行われ」→「おこなわれ」
# ※「行く」（いく）は補正対象外
```

### テキスト前処理

発音辞書と日本語読み補正の適用後、さらにテキスト前処理を行います。

| 記号 | 処理 | 理由 |
|------|------|------|
| `「」『』` | 除去 | 不要なポーズが入る |
| `（）()` | 除去 | 同上 |
| `～` | `ー` に置換 | 長音として正しく処理 |
| `・`（ナカグロ） | 文脈に応じて除去 or スペース | アクセント句境界の制御 |

さらに、40 文字を超える読点なしの文には、意味の切れ目に読点を自動補完します。これにより VOICEVOX のアクセント句が適切に分割され、イントネーションが自然になります。

### 感情別パラメータマトリクス

台本 JSON の `emotion` フィールドに応じて、音声パラメータを組み合わせます。`generate_audio.py` に定義されている `EMOTION_PARAMS` の抜粋です。

```python
EMOTION_PARAMS = {
    "normal":   {"speedScale": 1.1, "pitchScale": 0.0,
                 "intonationScale": 1.0, "pauseLengthScale": 1.0},
    "excited":  {"speedScale": 1.15, "pitchScale": 0.02,
                 "intonationScale": 1.2, "pauseLengthScale": 0.8},
    "sad":      {"speedScale": 0.95, "pitchScale": -0.02,
                 "intonationScale": 0.9, "pauseLengthScale": 1.3},
    "tsukkomi": {"speedScale": 1.15, "pitchScale": 0.03,
                 "intonationScale": 1.3, "pauseLengthScale": 0.8},
    "teaching": {"speedScale": 1.0, "pitchScale": 0.0,
                 "intonationScale": 1.1, "pauseLengthScale": 1.0},
    "gentle":   {"speedScale": 1.0, "pitchScale": -0.01,
                 "intonationScale": 0.9, "pauseLengthScale": 1.2},
    # ... 全 14 種類
}
```

各パラメータの効果を簡単に説明します。

| パラメータ | 効果 | 代表的な値 |
|-----------|------|-----------|
| `speedScale` | 話速。デフォルト 1.1 | excited: 1.15（速め）、sad: 0.95（遅め） |
| `pitchScale` | 音高のオフセット | excited: +0.02（高め）、sad: -0.02（低め） |
| `intonationScale` | 抑揚の振幅 | tsukkomi: 1.3（強い抑揚）、whisper: 0.8（抑え） |
| `pauseLengthScale` | ポーズ長 | excited: 0.8（短め）、sad: 1.3（長め） |

### 方言パラメータ

`dialect` フィールドが設定されているセリフには、`voicevox_params` で方言イントネーションを制御します。

```json
{
  "dialect": "osaka",
  "voicevox_params": {
    "speedScale": 1.2,
    "intonationScale": 1.3,
    "pitchScale": 0.02
  }
}
```

大阪弁と京都弁で異なるパラメータを使用します。

| 方言 | speedScale | intonationScale | pitchScale | 特徴 |
|------|-----------|----------------|------------|------|
| osaka（興奮系） | 1.2 | 1.3 | +0.02 | テンポ速め＋強い抑揚 |
| osaka（ツッコミ系） | 1.15 | 1.4 | +0.02 | より強い抑揚 |
| kyoto（はんなり） | 1.0 | 0.9 | -0.01 | ゆったり＋控えめな抑揚 |

### audio-pipeline の自動実行フロー

`audio-pipeline` スキルは、台本完了テーマの検出から PR マージまでを全自動で実行します。

```
Step 0:   環境準備・候補検出
Step 0.5: Phase 4 音声 Issue 番号の特定
Step 1:   ブランチ作成
Step 2:   発音辞書の更新
Step 3:   方言セリフの voicevox_params 確認
Step 4:   VOICEVOX 音声生成
Step 5:   Agent Teams レビュー（3 並列）
Step 6:   コミット＆push
Step 7:   セルフレビュー
Step 8:   PR 作成＆AI レビュー依頼
Step 9:   AI レビュー監視＆指摘対応
Step 10:  自動マージ
Step 11:  後処理（Issue クローズ・完了報告）
```

候補検出には `tools/discover_pending_audio.py` を使用します。このスクリプトは `content/scripts/{動画ID}_script.json` が main にマージ済みで、かつ `content/scripts/{動画ID}_timed.json` が存在しないテーマを検出します。

### 品質ゲート（尺チェック）

音声生成後、VOICEVOX の実測値で尺をチェックします。

| 実測尺 | 判定 | 対応 |
|--------|------|------|
| 8 分未満 | **NG** | パイプライン停止。Phase 3 差し戻し |
| 8〜10 分 | **WARN** | ユーザーに報告して判断を仰ぐ |
| 10〜20 分 | **OK** | 続行 |
| 20 分超 | **WARN** | ユーザーに報告して判断を仰ぐ |

8 分は YouTube ミッドロール広告の閾値です。8 分未満では収益機会を大きく損なうため、台本の根本的な見直しが必要です。

### 自動マージ条件

以下の全条件を満たす場合、ユーザー確認なしで自動マージします。

- 音声生成成功率 100%（エラー 0 件）
- 尺 8〜20 分
- セルフレビュー Error 0 件
- AI レビュー重大指摘なし

1 つでも条件を満たさない場合はマージせず、ユーザーに報告して判断を仰ぎます。

### Agent Teams レビュー

音声生成後、3 つの専門レビュアーを並列で起動します。

| レビュアー | 担当 |
|-----------|------|
| **方言イントネーション検証** | 大阪弁・京都弁セリフの accent_phrases ピッチパターン検証 |
| **標準語イントネーション検証** | 長文・疑問文の処理、感情パラメータマトリクス照合 |
| **発音・タイムド台本整合性** | 発音辞書カバレッジ、timed.json と音声ファイルの整合性 |

NG が 3 件以上残る場合はパイプラインを停止し、ユーザーに報告します。

### タイムド台本の出力

`generate_audio.py` は音声生成と同時に **タイムド台本**（`{動画ID}_timed.json`）を出力します。各セリフに `duration`（音声の長さ）、`start_sec`（開始時刻）、`end_sec`（終了時刻）が追加されます。

```json
{
  "id": "001",
  "text": "ねえきなこ、飼い主がまた新しいAIサービスに課金してるんだけど。",
  "duration": 3.42,
  "start_sec": 0.0,
  "end_sec": 3.42,
  "audio_file": "audio/V002/001.wav"
}
```

このタイムド台本が Remotion での動画レンダリングの入力になります。セリフ間のギャップ（デフォルト 0.3 秒）も自動計算されます。

---

## ハマりポイント

### 1. Git LFS と WAV ファイルの相性問題

当初、音声 WAV ファイルを Git LFS で管理しようとしましたが、Claude Code の実行環境がプロキシ経由のため LFS Batch API が 502 エラーを返す問題が発生しました。

抜本対策として、WAV ファイルは **LFS 対象外** としています。

```
# .gitattributes
assets/audio/**/*.wav !filter !diff !merge binary
```

セッション開始時には以下を実行して、LFS ダウンロードエラーによるブロックを回避します。

```bash
git lfs install --skip-smudge --local
```

### 2. 長母音の mora 表現差（偽陽性に注意）

VOICEVOX の `audio_query` が返す mora 表現では、長母音が変換されます。

| 辞書的表記 | VOICEVOX の mora | 実際の発音 |
|-----------|-----------------|----------|
| コウ | コオ | コー |
| エイ | エエ | エー |

発音検証スクリプトで「NG」と出ても、このパターンに該当する場合は **偽陽性** です。実際の音声は正しく発音されているため、無視して問題ありません。

### 3. `voicevox_params` の付け忘れ

`dialect` フィールドが設定されているのに `voicevox_params` がないセリフは、`generate_audio.py` が `DIALECT_DEFAULTS` のフォールバック値を適用します。しかしこの場合、興奮系 / ツッコミ系の区別ができません。台本側で明示設定することが重要です。

`post-tool-use-validate.sh`（Lv3 フック）が台本 JSON 書き込み時に自動で警告を出すため、通常は見落としません。

---

## まとめ

Phase 4-A の音声生成パイプラインは、以下の 3 層で合成音声の品質を確保しています。

- **発音辞書**: 英語用語・難読語のカタカナ / ひらがな置換で基本的な発音を制御
- **日本語読み補正**: 正規表現ベースで「数 + 助数詞」等の体系的な誤読を補正
- **パラメータ最適化**: 感情マトリクス・方言パラメータで表現力を付与

`audio-pipeline` スキルにより、台本完了テーマの検出から PR マージまでを全自動で実行します。品質ゲート（尺チェック・Agent Teams レビュー・セルフレビュー・AI レビュー）を通過した音声のみが自動マージされ、品質基準を満たさない場合は人間にエスカレーションされます。

次のチャプターでは、Gemini API を使った画像素材の自動生成（Phase 4-B）を解説します。
