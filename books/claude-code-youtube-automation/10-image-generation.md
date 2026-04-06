---
title: "Phase 4-B — 画像生成（Gemini API）"
---

## このチャプターで学ぶこと

- Gemini API（gemini-3.1-flash-image-preview）を画像生成モデルに選定した理由
- 台本の `visual_cue` フィールドから画像を自動生成するフローの全体像
- デザイン定義書によるキャラクターの一貫性担保の仕組み
- `imageMap.ts` によるセリフID → 画像パスのマッピング設計
- サムネイル自動生成の評価基準と赤アラート＋黄バナースタイル
- image-pipeline スキルによる全自動実行の流れ

---

## 背景・課題 — なぜ画像生成が必要なのか

テック解説動画において、視覚情報は視聴者の理解と視聴維持率に直結します。グラフ、図解、プロフィールカード、タイトルカードなど、セリフごとに適切なビジュアルを表示することで、音声だけでは伝えきれない情報を補完できます。

しかし、15〜20分の動画には30〜50枚もの画像素材が必要です。これを毎回手作業で作成していては、制作のボトルネックになります。本プロジェクトでは、台本に記述された `visual_cue`（視覚指示）をもとに、Gemini API で画像を自動生成する仕組みを構築しました。

### 解決すべき課題

1. **量の問題**: 1動画あたり30〜50枚の画像を毎回生成する必要がある
2. **一貫性の問題**: キャラクターのデザインが画像ごとにブレてはいけない
3. **テキスト描画の問題**: 画像内に正確な日本語テキストを含める必要がある
4. **品質管理の問題**: 文字化けや品質の低い画像を自動検出・再生成する仕組みが必要

---

## 設計思想

### Gemini API を選んだ理由

画像生成モデルの選定では、以下の比較を行いました。

| モデル | 日本語テキスト描画 | API の柔軟性 | コスト |
|--------|----------------|------------|--------|
| DALL-E 3 | △ 日本語が崩れやすい | ○ | 高い |
| Stable Diffusion | × 日本語は苦手 | ○ | 低い |
| **gemini-3.1-flash-image-preview** | **◎ 精度が高い** | **○ MCP 経由で統合** | **低い** |

最終的に `gemini-3.1-flash-image-preview` を採用しました。決め手は **日本語テキストの描画精度** です。テック解説動画ではグラフの軸ラベルやタイトルカードに日本語テキストを含めることが多く、他のモデルでは文字化けが頻発しました。

:::message
画像生成は MCP サーバー（`mcp__gemini-image__generate_image`）経由で実行します。直接 Gemini API を呼び出すスクリプトを新規作成することは禁止しています。認証やエラーハンドリングが MCP サーバーにカプセル化されているためです。
:::

### visual_cue → 画像生成の変換フロー

台本 JSON の各セリフには `visual_cue` フィールドがあり、そのセリフで表示すべきコンテンツを日本語で指示します。

```json
{
  "id": "024",
  "character": "kinako",
  "text": "この研究、16名の開発者を対象にしたランダム化比較試験なの。",
  "visual_cue": "METR研究の概要を表示（16名のOSS開発者、246タスク、ランダム化比較試験）"
}
```

この `visual_cue` を Gemini API のプロンプトに変換し、画像を生成します。変換の流れは以下のとおりです。

```
台本JSON の visual_cue（日本語の説明文）
  ↓ デザイン定義書のテンプレートと合成
プロンプト（英語ベース + kawaii スタイル指示）
  ↓ mcp__gemini-image__generate_image
base64 エンコードされた画像データ
  ↓ デコード＆保存
assets/images/V{id}/{セリフID}_{説明}.png
  ↓ imageMap.ts に登録
Remotion でセリフに同期表示
```

:::message
`visual_cue` の3状態（値あり・`null`・空文字）の詳細は Ch.08「台本生成」の `visual_cue` の3状態セクションを参照してください。
:::

---

## 実装詳細

### デザイン定義書によるキャラクター一貫性の担保

全画像で統一されたキャラクターデザインを維持するため、`docs/design-spec.md` にデザイン定義書を用意しています。

画像生成プロンプトの先頭には、必ず以下の共通スタイルベースを付与します。

```
Style: kawaii Japanese chibi illustration, 2-2.5 head proportion,
bold clean black outlines, soft cel shading, pastel-bright warm
color palette, simple details, white background. 2D illustration,
NOT realistic, NOT 3D render, NOT watercolor.
```

キャラクターを含む画像には、さらに一貫性指示を追加します。

```
IMPORTANT: Character eyes must be drawn as simple big round dark
brown circles with exactly two white circular highlights (one large,
one small). Do NOT draw detailed/realistic pupils, iris patterns,
or anime-style complex eyes.
```

:::message
キャラクターの一貫性で特に崩れやすいのは「目の描写」です。プロンプトが長くなると末尾の指示が無視されやすいため、アクセサリー（もっちーの青バンダナ、きなこの丸メガネ＋紫スカーフ）の指示はプロンプト前半に配置しています。
:::

### imageMap.ts の設計

`imageMap.ts` はセリフID と画像ファイルパスを対応づけるマッピングファイルです。動画ごとに `remotion/src/data/V{id}/imageMap.ts` に配置します。

```typescript
// remotion/src/data/V001/imageMap.ts
import { staticFile } from "remotion";

export const imageMap: Record<string, string> = {
  "010": staticFile("images/V001/010_karpathy_profile.png"),
  "015": staticFile("images/V001/015_metr_study_overview.png"),
  "024": staticFile("images/V001/024_comparison_graph.png"),
  // ... 全 visual_cue のセリフID を登録
};
```

Remotion の `VisualCue` コンポーネントは、現在のセリフID で `imageMap` を検索し、対応する画像があればタブレットフレーム内に表示します。画像がない場合のみ、テキストカード（`textContentMap`）をフォールバックとして使用します。

**設計上のルール**:
- `backgrounds/` パスのファイルは登録しない（背景は `Background` コンポーネントが担当）
- opening セクションの冒頭セリフ（フック）の `visual_cue` は登録しない（背景＋キャラのみ）
- 全ての `visual_cue` に対して画像を生成し、テキストカードをメイン表示に使わない

### Remotion のデータディレクトリ構造

各動画のデータは以下の構造で管理します。

```
remotion/src/data/V{id}/
├── index.ts         # VideoData をエクスポート
├── imageMap.ts      # セリフID → 画像パス
├── textContent.tsx  # テキストカード（フォールバック用）
├── sourceMap.ts     # セリフID → 出典情報
└── config.ts        # フルスクリーン設定
```

新しい動画を追加する際は、`remotion/src/data/index.ts` のレジストリに登録します。

```typescript
// remotion/src/data/index.ts
const VIDEO_DATA_REGISTRY: Record<string, VideoData> = {
  V001: v001Data,
  V002: v002Data,
  V003: v003Data,
};
```

### サムネイル生成 — 赤アラート＋黄バナースタイル

サムネイルはチャンネルの「顔」です。V001 での検証結果から、**赤アラート＋黄バナースタイル**（ゆっくり解説風）を全動画の標準スタイルとして採用しました。

**スタイルの特徴**:
- **背景**: ダーク系（黒〜深紅のグラデーション）＋斜めスピードライン
- **Line 1**: 白テキスト＋黒アウトライン（補足ワード、5〜10文字）
- **Line 2**: 黄色バナー内の黒テキスト＋赤い「？」「！」（キーワード、2〜5文字）
- **キャラクター**: 隅に小さく配置（15〜20%）

テキストの役割分担が重要です。

| 要素 | 役割 | 例 |
|------|------|-----|
| 動画タイトル | 何についての動画か | `バイブコーディングは終わった？...` |
| サムネテキスト | なぜ見るべきか | Line 1: `バイブコーディング` / Line 2: `終了？` |

### 6軸評価基準によるサムネイル品質管理

生成されたサムネイルはサブエージェントが6軸で評価し、品質を担保します。

| 基準 | 評価内容 |
|------|---------|
| デザイン統一性 | kawaii スタイルとの一貫性 |
| テキスト視認性 | 黄バナーの正確さ、テキストの読みやすさ |
| テーマ関連性 | 動画テーマとの関連性 |
| クリック誘引力 | 視覚的インパクト |
| キャラクター品質 | アクセサリーの描画品質 |
| モバイル視認性 | 120×90px 縮小時の可読性 |

合計60点満点で **42点以上** が自動採用基準です。42点未満の場合は最大3サイクルまで再生成します。

### image-pipeline の自動実行フロー

`/image-pipeline` スキルは以下のステップで全自動実行します。

```
Step 0: 準備（ブランチ作成・環境変数確認）
Step 1: Remotion データディレクトリ作成（imageMap.ts 等）
Step 2: 全 visual_cue の画像を一括生成（MCP ツール経由）
Step 3: BGM トラック確認・追加
Step 4: サムネイル生成（6軸評価 42点以上まで再生成）
Step 5: コミット＆push
Step 6: セルフレビュー
Step 7: PR作成 → AIレビュー → 自動監視
Step 8: 自動マージ → 次Phase Issue作成
```

自動マージの条件は厳格です。

| 条件 | 基準 |
|------|------|
| 画像生成成功率 | 100%（全 visual_cue の画像が存在） |
| imageMap.ts 登録 | 全セリフIDが登録済み |
| TypeScript コンパイル | エラー 0 件 |
| セルフレビュー | Error 0 件 |
| AIレビュー | 重大指摘なし |

1つでも条件を満たさない場合は自動マージせず、ユーザーに報告して判断を仰ぎます。

---

## ハマりポイント

### 1. テキスト文字化けとの戦い

Gemini API でも日本語テキストの文字化けは完全には防げません。特に以下のケースで発生しやすいです。

- **長い日本語テキスト**: 10文字を超えると崩れやすくなる
- **プロンプトが長い場合**: 末尾のテキスト指示が無視される

対策として、全画像に対して生成後に文字化けチェックを実施し、NG の場合は最大3回再生成します。3回でも改善しない場合はテキストなし画像を生成し、Remotion 側でテキストオーバーレイする方針に切り替えます。

### 2. backgrounds/ パスの imageMap 登録ミス

初期の実装で `backgrounds/` パスのファイルを `imageMap.ts` に登録してしまい、背景画像が二重表示される問題が発生しました。背景は `Background` コンポーネント（z-index 0）が担当するため、`imageMap.ts` には `images/V{id}/` 配下のファイルのみを登録する必要があります。セルフレビューでこのパターンを自動検出するチェックを追加しました。

### 3. MCP サーバー認証エラーのハンドリング

Gemini API の MCP サーバーは `GEMINI_MCP_AUTH_TOKEN` 環境変数で認証します。クラウド環境（Claude Code Scheduled Tasks）ではセッションごとに環境がリセットされるため、環境変数の設定漏れでパイプラインが停止することがありました。Step 0 で環境変数の存在を必ず確認し、未設定の場合は即座に STOP する設計にしています。

---

## まとめ

- Gemini API（gemini-3.1-flash-image-preview）は日本語テキスト描画精度が最も高く、テック解説動画の画像生成に最適です
- デザイン定義書と共通プロンプトベースにより、全画像でキャラクターデザインの一貫性を維持しています
- `imageMap.ts` によるセリフID → 画像パスのマッピングで、Remotion が台本に同期した画像表示を実現しています
- サムネイルは6軸評価基準で自動採点し、42点以上で自動採用する品質管理を導入しています
- image-pipeline は全8ステップを自動実行し、全条件を満たせばユーザー確認なしで自動マージします
