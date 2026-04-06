---
title: "Phase 6.5 — SNS配信"
---

## このチャプターで学ぶこと

- マルチプラットフォーム配信戦略の設計思想（Zenn, note, Qiita, X, Bluesky）
- Zenn 記事の自動生成フロー（台本JSON → Markdown → GitHub push → 自動公開）
- note 有料記事ドラフトの自動生成と無料/有料部分の自動分割ロジック
- 多言語対応（英語タイトル・説明・字幕の自動生成）
- sns-publisher スキルによる5プラットフォーム並列配信のオーケストレーション

---

## 背景・課題 — なぜマルチプラットフォーム配信が必要か

YouTube 動画を公開しただけでは、リーチできる層は限られます。テック系のコンテンツは、動画を見ない層（記事で読みたい人）や、特定のプラットフォームにしかいない層にも需要があります。

1つの動画コンテンツを複数のプラットフォームに展開することで、以下の効果が期待できます。

| 効果 | 説明 |
|------|------|
| SEO の二重露出 | Zenn 記事が Google 検索にヒット → YouTube への流入 |
| 収益の多角化 | note 有料記事による直接的な収益 |
| コミュニティリーチ | Qiita でテックコミュニティへの認知拡大 |
| リアルタイム告知 | X / Bluesky での公開告知と議論 |

しかし、同じ内容を5つのプラットフォームに手動で展開するのは現実的ではありません。台本 JSON という構造化データがあるからこそ、各プラットフォームに最適化したコンテンツを自動生成できます。

---

## 設計思想

### プラットフォーム役割分担

各プラットフォームには明確な役割を割り当てています。「全部に同じ内容を投稿する」のではなく、プラットフォームの特性に合わせたコンテンツ差別化を行います。

| プラットフォーム | 役割 | 自動化レベル | 収益化 |
|----------------|------|------------|--------|
| **Zenn** | 動画内容の記事化（無料） | 全自動（GitHub 連携） | バッジのみ |
| **note** | 詳細解説（有料） | 半自動（ドラフト生成→手動公開） | 有料記事 |
| **Qiita** | 最新情報の早期配信 | 全自動（API v2） | なし |
| **X** | 動画告知 | 全自動（API） | なし |
| **Bluesky** | テック層への告知 | 全自動（AT Protocol） | なし |

### コンテンツの差別化原則

```
YouTube 動画（メインコンテンツ）
  ├── Zenn: 概要 + ポイント（無料・認知拡大）
  ├── note: 詳細解説 + 実装ガイド（有料・収益化）
  ├── Qiita: 技術的ポイントに特化（無料・コミュニティ）
  ├── X: 短文告知 + スレッド（リアルタイム）
  └── Bluesky: テック層向け告知（エンゲージメント）
```

:::message
Zenn 書籍（本書）と Zenn 記事は別物です。書籍は体系的な教科書として制作パイプライン全体を解説し、記事は各動画の内容を個別に記事化します。同じ内容の転載は行いません。
:::

---

## 実装詳細

### Zenn 記事の自動生成

Zenn は GitHub リポジトリとの連携機能を持っており、`articles/` ディレクトリに Markdown ファイルを push するだけで自動公開されます。この仕組みを活用して完全自動化しています。

**自動化の流れ**:

```
台本 JSON（content/scripts/{VIDEO_ID}_script.json）
  ↓ tools/generate_zenn_article.py
Markdown ファイル（/tmp/zenn-articles/{SLUG}.md）
  ↓ Agent Teams レビュー（3レビュアー並列）
品質確認済み Markdown
  ↓ git push（Zenn 連携リポジトリ）
Zenn が検出して自動公開
```

`tools/generate_zenn_article.py` は台本 JSON を解析し、以下の変換を行います。

```bash
python tools/generate_zenn_article.py V001 \
  --youtube-url https://youtu.be/xxxxx \
  --output-dir /tmp/zenn-articles
```

**変換ロジックの要点**:

1. **定番枠の除外**: `title_call` と `cta` セクションは記事には不要なのでスキップ
2. **短い相槌の除外**: 15文字未満のリアクション行（「うん」「なるほど」等）は除外
3. **セクション単位の要約**: 各セクションのセリフを箇条書き（最大6項目）に凝縮
4. **Zenn タグの自動マッピング**: 台本のキーワードを Zenn の topics 形式に変換

```python
# tools/generate_zenn_article.py より
ZENN_TAG_MAP = {
    "AI": "ai",
    "LLM": "llm",
    "バイブコーディング": "vibe-coding",
    "Cursor": "cursor",
    "ClaudeCode": "claude",
    # ...
}

# 定番枠スキップ
SKIP_SECTIONS = {"title_call", "cta"}
```

生成される Markdown の frontmatter は以下の形式です。

```markdown
---
title: "バイブコーディングは終わった？【解説記事】"
emoji: "🐹"
type: "tech"
topics: ["vibe-coding", "ai", "claude", "llm"]
published: true
---
```

**Agent Teams レビュー**: push 前に3つの専門レビュアーが並列で品質チェックします。

| レビュアー | チェック観点 |
|-----------|------------|
| コンテンツレビュアー | 記事内容と動画の一致、ハルシネーション検出 |
| SEO/タグレビュアー | topics・タイトル・emoji の適切さ |
| 品質レビュアー | 構成・箇条書き・Zenn 形式の適合確認 |

全員 OK ならそのまま push、NG が1〜2件なら自動修正して1回のみ再確認します。自動修正は1サイクルのみ（サーキットブレーカー）で、それでも NG なら STOP してユーザーに報告します。

### note 有料記事ドラフトの自動生成

note は API での記事投稿ができないため、ドラフト生成までを自動化し、投稿はユーザーが手動で行います。

```bash
python tools/generate_note_draft.py V001 \
  --youtube-url https://youtu.be/xxxxx
```

**無料/有料部分の自動分割ロジック**:

```python
# tools/generate_note_draft.py より
PAID_SECTION_KEYWORDS = [
    "実装", "仕組み", "技術", "アーキテクチャ",
    "詳細", "手順", "方法", "実践", "ツール",
    "API", "プロンプト", "設計", "比較", "評価",
]
```

セクション名に上記のキーワードが含まれていれば「有料部分」として分類します。opening や概要は無料部分に配置し、技術的な深い内容は有料部分に回します。

**価格の自動判断**: 台本の文字数に応じて推奨価格を算出します。

```python
def suggest_price(total_chars: int) -> int:
    if total_chars < 3000:
        return 500
    elif total_chars < 5000:
        return 1000
    elif total_chars < 7000:
        return 1500
    else:
        return 2000
```

生成されたドラフトは `content/note/{VIDEO_ID}_note_draft.md` に保存されます。ユーザーは note.com に手動で貼り付け、有料ラインを設定して公開します。

### Qiita・X・Bluesky の自動投稿

これらのプラットフォームは API による自動投稿に対応しています。各ツールは環境変数が設定されている場合のみ実行し、未設定の場合はスキップします。

**Qiita** (`tools/post_qiita_article.py`):
- Qiita API v2 で記事を自動投稿
- タグは `QIITA_TAG_MAP` で Qiita 対応形式に変換
- 環境変数: `QIITA_TOKEN`

**X** (`tools/post_x_announcement.py`):
- OAuth 1.0a で認証、動画告知をスレッド形式で投稿
- `--thread` オプションでスレッド投稿（1ツイート目に動画リンク、2ツイート目以降にポイント）
- 環境変数: `X_API_KEY` / `X_API_SECRET` / `X_ACCESS_TOKEN` / `X_ACCESS_TOKEN_SECRET`
- Basic プラン以上が必要（Free プランでは POST /tweets が使えない）

**Bluesky** (`tools/post_bluesky.py`):
- AT Protocol API で認証・投稿
- 環境変数: `BLUESKY_HANDLE` / `BLUESKY_APP_PASSWORD`
- ハンドルは `yourname.bsky.social` 形式（`@` は不要）

### 多言語対応

本プロジェクトでは単一チャンネルで多言語対応する方針を取っています。YouTube Data API v3 の `localizations` 機能と多言語字幕で海外視聴者にリーチします。

**英語タイトルの生成ルール**:

日本語タイトルの直訳ではなく、英語圏の SEO に最適化した独自タイトルを生成します。

| 日本語 | 英語（NG: 直訳） | 英語（OK: SEO最適化） |
|--------|----------------|-------------------|
| バイブコーディングは終わった？ | Is Vibe Coding Over? | Is Vibe Coding Dead? AI Coding 2026 |
| AI生成コードの45%に脆弱性！ | 45% of AI Generated Code... | AI Code Security Crisis: 45% Vulnerable |

メインキーワードはタイトル先頭5語以内に配置し、全体60文字以内（英語は日本語より長くなるため上限を緩和）に収めます。

**localizations API の設定**:

```python
youtube.videos().update(
    part="localizations",
    body={
        "id": youtube_video_id,
        "localizations": {
            "en": {
                "title": "Is Vibe Coding Dead? AI Coding 2026",
                "description": "Mocchii the hamster and Kinako..."
            }
        }
    }
).execute()
```

**対応言語の優先順位**:

| 優先度 | 言語 | 対応フェーズ |
|--------|------|------------|
| 1 | 英語 | 即時対応 |
| 2 | ポルトガル語・スペイン語 | 英語圏視聴5%達成後 |
| 3 | 韓国語・繁体中国語・ドイツ語・フランス語 | 需要に応じて |

### sns-publisher のオーケストレーション

`/sns-publisher` スキルは5つのプラットフォームへの配信を並列で実行します。

```
Step 0: 対象動画の確認（公開済み＆SNS未配信の動画を自動検出）
Step 1: 前提確認（台本・メタデータの存在）
Step 2: 並列実行（5サブエージェント同時起動）
  ├── Step 2-A: Zenn 記事生成
  ├── Step 2-B: note ドラフト生成
  ├── Step 2-C: Qiita 記事投稿
  ├── Step 2-D: X 投稿
  └── Step 2-E: Bluesky 投稿
Step 2.5: Zenn 記事の Agent Teams レビュー
Step 3: Zenn リポジトリへ push
Step 4: sns_urls.yaml に全 URL を記録
Step 5: YouTube 概要欄に SNS リンクを追記
Step 6: コミット & PR 作成
```

配信結果は `content/meta/{VIDEO_ID}_sns_urls.yaml` に記録します。

```yaml
video_id: V001
youtube_url: https://www.youtube.com/watch?v=xxxxx
zenn_url: https://zenn.dev/kinamocchi_tech/articles/kinamocchi-v001
note_draft: content/note/V001_note_draft.md
note_url: null  # ユーザーが手動公開後に記入
qiita_url: https://qiita.com/xxx/items/yyy
x_post_url: https://x.com/xxx/status/yyy
bluesky_url: https://bsky.app/profile/xxx/post/yyy
```

---

## ハマりポイント

### 1. Zenn の topics 制約

Zenn の `topics` は英数字とハイフンのみ使用可能で、日本語のタグは受け付けません。台本のキーワード（「バイブコーディング」「AIエージェント」等）をそのまま使うと記事が正しく公開されません。

`ZENN_TAG_MAP` で日本語キーワードを Zenn 対応のスラッグに変換しています。新しいキーワードが登場したらマップに追加する運用が必要です。

```python
ZENN_TAG_MAP = {
    "バイブコーディング": "vibe-coding",
    "AIエージェント": "ai",
    "プロンプトエンジニアリング": "prompt-engineering",
}
```

### 2. X API のプラン制約

X (Twitter) の Free プランでは `POST /tweets` エンドポイントが使えません。Basic プラン（月額 $100）以上が必要です。環境変数が設定されていても API アクセスレベルが不足すると `403 Forbidden` が返ります。スキルは環境変数の有無だけでなく、最初の投稿試行時のレスポンスコードで判断しています。

### 3. note の有料ライン設定

note のドラフトは Markdown で生成しますが、note の有料ラインは Markdown 上では表現できません。ドラフト内にコメント（`<!-- 有料ライン -->`）としてマーカーを配置し、ユーザーが note.com のエディタで手動設定する運用にしています。完全自動化は note の API 制約上、現状では不可能です。

---

## まとめ

- 5つのプラットフォーム（Zenn, note, Qiita, X, Bluesky）に役割を分担し、コンテンツを差別化して配信しています
- Zenn は GitHub 連携による完全自動公開、note は半自動（ドラフト生成→手動公開）で運用しています
- 台本 JSON という構造化データがあるからこそ、各プラットフォームに最適化したコンテンツ変換が可能です
- 5つのサブエージェントを並列起動することで、配信の所要時間を最小化しています
- 多言語対応は YouTube の localizations API を活用し、英語を最優先で展開しています
- 配信結果は `sns_urls.yaml` に一元記録し、トレーサビリティを確保しています
