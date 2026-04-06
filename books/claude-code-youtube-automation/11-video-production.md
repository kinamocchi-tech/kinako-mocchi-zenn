---
title: "Phase 5 — 動画制作（Remotion）"
---

## このチャプターで学ぶこと

- Remotion を動画制作フレームワークに選定した理由
- レイヤー構成（z-index）による画面設計の全体像
- VisualCue の表示ルール（null=継続、""=クリア）
- JIS X 4051 禁則処理に基づく字幕改行アルゴリズム
- フルスクリーンモードの実装パターン
- remotion-render スキルの実行フローと品質チェック

---

## 背景・課題 — なぜ Remotion なのか

従来の動画制作は Adobe Premiere Pro や DaVinci Resolve といった GUI ベースのツールが主流です。しかし、AI 駆動の自動化パイプラインでは「プログラムから動画を生成する」能力が必要です。

### GUI ツールの限界

- 台本の変更に対して手動で全セリフのタイミングを再調整する必要がある
- キャラクターアニメーションのパターンを手作業で適用する必要がある
- CI/CD パイプラインに組み込めない

### Remotion の利点

[Remotion](https://www.remotion.dev/) は React コンポーネントで動画を構築するフレームワークです。

| 特徴 | メリット |
|------|---------|
| React ベース | Web 開発者が馴染みやすい。TypeScript で型安全 |
| プログラマブル | JSON データから動的に動画を生成できる |
| コンポーネント指向 | 背景・キャラ・字幕を独立したレイヤーで管理 |
| CLI レンダリング | `npx remotion render` でヘッドレス動画出力 |

本プロジェクトでは、タイムド台本（`*_timed.json`）を入力として Remotion が動画を自動生成します。台本を修正すれば、再レンダリングだけで動画が更新されます。

---

## 設計思想

### レイヤー構成（z-index）

画面は6つのレイヤーで構成されています。z-index が大きいほど前面に表示されます。

| z-index | コンポーネント | 役割 |
|---------|--------------|------|
| 0 | `Background` | 背景画像（ホームオフィス風） |
| 1 | `VisualCue` + `TabletFrame` | コンテンツエリア（画像 or テキストカード） |
| 2 | `Character` | もっちー・きなこの立ち絵 |
| 3 | `Subtitle` | 字幕テロップ |
| 4 | `SourceCredit` | 出典情報バッジ（左上固定） |
| 5 | `EndingCredits` | エンディングクレジット（ending セクション中のみ表示） |

```
┌──────────────────────────────────────────┐
│  [出典: SourceCredit]     ← z-index 4   │
│                                          │
│  ┌──────────────────────────────────┐    │
│  │  タブレットフレーム  ← z-index 1  │    │
│  │  （画像 or テキストカード）       │    │
│  └──────────────────────────────────┘    │
│                                          │
│  [もっちー]           [きなこ]           │
│  ← z-index 2（キャラがコンテンツ上に）   │
│                                          │
│  ┌──────────────────────────────────┐    │
│  │    字幕テロップ     ← z-index 3   │    │
│  └──────────────────────────────────┘    │
└──────────────────────────────────────────┘
```

キャラクター（z-index 2）がコンテンツ（z-index 1）よりも前面に来るのがポイントです。キャラクターがタブレットを「覗き込んでいる」ような自然な見た目になります。

### コンポーネント構成

```
remotion/src/
├── index.ts                  # registerRoot
├── Root.tsx                  # Composition 定義（動画ID別）
├── KinakoMocchiiVideo.tsx    # メインオーケストレーター
├── types.ts                  # TimedLine / TimedScript 型定義
├── utils/
│   └── subtitleSplit.ts      # 字幕分割ロジック
├── components/
│   ├── Background.tsx        # 背景画像
│   ├── Character.tsx         # キャラクター立ち絵 + アニメーション
│   ├── Subtitle.tsx          # 字幕テロップ
│   ├── VisualCue.tsx         # コンテンツエリア
│   ├── TabletFrame.tsx       # タブレット風フレーム
│   ├── SourceCredit.tsx      # 出典情報バッジ
│   ├── EndingCredits.tsx     # エンディングクレジット
│   └── cards.tsx             # テキストカード各種
└── data/
    ├── index.ts              # 動画データレジストリ
    └── V{id}/                # 動画別データ
```

### 型定義（types.ts）

タイムド台本の構造を TypeScript で厳密に型定義しています。

```typescript
export interface TimedLine {
  id: string;
  character: Character;       // "mocchii" | "kinako"
  emotion: Emotion;           // "normal" | "excited" | "tsukkomi" | ...
  text: string;
  action: Action;             // "idle" | "jump" | "shake" | ...
  visual_cue: string | null;
  audio_file: string;
  duration_sec: number;
  start_sec: number;
  end_sec: number;
}

export interface TimedScript {
  video_id: string;
  title: string;
  lines: TimedLine[];
  total_duration_sec: number;
  bgm_tracks?: BgmTrack[];
}
```

---

## 実装詳細

### VisualCue の表示ルール

`KinakoMocchiiVideo.tsx` の `getActiveVisualCue()` 関数が、現在のフレームに対してどの visual_cue を表示するかを決定します。

```typescript
function getActiveVisualCue(
  lines: TimedLine[],
  frame: number,
  fps: number
): { lineId: string; visualCue: string; changedFrame: number } | null {
  let lastCueLineId: string | null = null;
  let lastCue: string | null = null;
  let lastCueFrame = 0;

  for (const line of lines) {
    const startFrame = Math.round(line.start_sec * fps);
    if (startFrame > frame) break;

    if (line.visual_cue === "") {
      // 空文字 = 意図的クリア
      lastCueLineId = null;
      lastCue = null;
    } else if (line.visual_cue != null) {
      // 新しい visual_cue
      lastCueLineId = line.id;
      lastCue = line.visual_cue;
      lastCueFrame = startFrame;
    }
    // null の場合は直前を継続（何もしない）
  }
  // ...
}
```

:::message
`null` と `""` の使い分けが重要です。`null` は「同じ話題の続きだから前の画像を維持」、`""` は「話題が完全に切り替わるから画像をクリア」を意味します。台本作成時にこの区別を意識することで、自然な画面遷移を実現できます。
:::

### 字幕改行ルール — JIS X 4051 禁則処理 + 均等分割

字幕の改行は `utils/subtitleSplit.ts` の `splitSubtitleLines()` で処理します。日本語組版の標準規格 JIS X 4051 の禁則処理を実装しつつ、独自の均等分割ロジックを加えています。

**基本定数**:

```typescript
export const MAX_LINE = 22;   // 1行の最大文字数
export const MAX_LINES = 3;   // 最大行数
```

**分割禁止条件**（`isSafeSplitPoint()` が `false` を返すケース）:

```typescript
// subtitleSplit.ts より抜粋（境界チェック等は省略）
export function isSafeSplitPoint(text: string, pos: number): boolean {
  const before = text[pos - 1];
  const after = text[pos];

  // 行頭禁則文字
  if (LINE_START_PROHIBITED.has(after)) return false;

  // 英数字の連続中（英単語・URL の途中）
  if (/[a-zA-Z0-9]/.test(before) && /[a-zA-Z0-9]/.test(after))
    return false;

  // カタカナ語の途中
  if (/[\u30A0-\u30FF]/.test(before) && /[\u30A0-\u30FF]/.test(after))
    return false;

  // 数値 + 日本語単位の途中（2025年、50% など）
  if (/[0-9]/.test(before) && /[年月日%]/.test(after))
    return false;

  return true;
}
```

**均等分割アルゴリズム**: ターゲット位置（残りテキスト÷残り行数）を中心に ±8 文字の範囲で最適な分割点を探索します。1行目が極端に短く3行目にテキストが集中する問題を防ぎます。

**探索の優先順位**:
1. ターゲット付近の文末記号（`。！？`）の直後
2. ターゲット付近の読点（`、`）の直後
3. ターゲット付近の安全分割点
4. フォールバック: ターゲット位置で強制分割

**動的フォントスケーリング**: 行の推定描画幅がテキストエリアを超える場合、フォントサイズを自動縮小します。半角英数字は全角の0.55倍の幅で概算します。

```typescript
function estimateLineWidth(line: string, fontSize: number): number {
  let width = 0;
  for (const ch of line) {
    width += ch.charCodeAt(0) <= 0x7f ? fontSize * 0.55 : fontSize;
  }
  return width;
}
```

### 字幕テキスト色ルール

キャラクターごとに字幕の色を変えることで、誰が話しているか視覚的に区別できます。

```typescript
const CHARACTER_COLORS: Record<Character, string> = {
  mocchii: "#FF8C42",  // オレンジ
  kinako: "#4CAF7A",   // 緑
};
```

フルスクリーンモードでは背景画像との視認性を確保するため、常に白（`#FFFFFF`）を使用します。

### フルスクリーンモード

チャンネルタイトルコールや CTA（Call To Action）シーンでは、画像を画面全体に表示してキャラクターを非表示にします。

```typescript
const FULLSCREEN_CUE_IDS = new Set(["006", "098", "099", "100"]);
const FULLSCREEN_LINE_IDS = new Set(["006", "007"]);

const isFullscreen =
  (activeVisualCue?.lineId != null &&
    FULLSCREEN_CUE_IDS.has(activeVisualCue.lineId)) ||
  (currentLine?.id != null &&
    FULLSCREEN_LINE_IDS.has(currentLine.id));
```

**2つの集合の使い分け**:

| 集合 | 用途 | 判定方法 |
|------|------|---------|
| `FULLSCREEN_CUE_IDS` | `visual_cue` を持つセリフ | 後続の `null` セリフも自動継続 |
| `FULLSCREEN_LINE_IDS` | `visual_cue=""` で直接指定が必要なセリフ | 個別に追加 |

フルスクリーンモードの字幕は「浮動テキスト」になります。枠なしで画像下部にグラデーション帯を敷き、白テキストを表示します。

### キャラクターアニメーション

キャラクターのアニメーションは Remotion の `spring()` と `interpolate()` で CSS Transform を適用します。

```typescript
import { spring, interpolate, useCurrentFrame, useVideoConfig } from "remotion";
```

| アクション | 変換内容 |
|-----------|--------|
| `idle` | 微かな上下揺れ（呼吸） |
| `jump` | spring() で Y 軸ジャンプ |
| `spin` | rotate 360° |
| `shake` | X 軸の往復振動 |
| `nod` | Y 軸の小さな上下 |
| `tilt_head` | rotate ±15° |
| `flap` | Y 軸の羽ばたき + 回転（きなこ用） |

### レンダリング手順

```bash
# Step 1: プレビュー確認
cd remotion && npx remotion preview

# Step 2: ドラフトレンダリング
npx remotion render src/index.ts V001 \
  --output ../output/V001_draft.mp4

# Step 3: 品質チェック後、最終レンダリング
npx remotion render src/index.ts V001 \
  --output ../output/V001.mp4 \
  --codec h264 --crf 18
```

### SourceCredit（出典表示）

情報の信頼性を視聴者に示すため、画面左上に出典情報を表示します。

| ランク | バッジ色 | 意味 |
|--------|--------|------|
| [公式] | 緑 `#4CAF7A` | 公式ブログ・論文 |
| [報道] | 青 `#5BC0F8` | 大手メディア記事 |
| [参考] | 黄 `#FFD700` | コミュニティ情報 |

`visual_cue` が切り替わるタイミングでフェードインし、同じ `visual_cue` が続く限り表示を維持します。URL が長い場合はスクロールアニメーション（1秒待機→5秒スクロール→1秒ホールド）をリピートします。

---

## ハマりポイント

### 1. カタカナ語の途中改行

「バイブコーディング」のような長いカタカナ語が字幕の途中で改行されると、非常に読みにくくなります。`isSafeSplitPoint()` でカタカナ連続（`[\u30A0-\u30FF]`）の間を分割禁止にすることで解決しました。

ただし、これにより分割可能な位置が制限され、行が MAX_LINE を超えることがあります。その場合は動的フォントスケーリングが発動し、フォントサイズを縮小して1行に収めます。

### 2. FULLSCREEN_CUE_IDS と FULLSCREEN_LINE_IDS の混同

`visual_cue` を持つセリフを `FULLSCREEN_LINE_IDS` に追加しても、後続の `visual_cue=null` セリフでフルスクリーンが維持されません。逆に、`FULLSCREEN_CUE_IDS` に追加すれば後続セリフも自動的にフルスクリーンになります。この使い分けを間違えると、CTA シーンの途中でキャラクターが突然表示されるバグになります。

### 3. 既存動画データの保護

新しい動画のデータを追加する際に、既存動画（V001 等）の `remotion/src/data/` を変更してしまうと、過去の動画のレンダリング結果が変わってしまいます。動画データレジストリ（`data/index.ts`）は追加のみで、既存エントリの変更は禁止しています。

---

## まとめ

- Remotion は React コンポーネントで動画を構築でき、JSON データからの自動生成に最適です
- 6層のレイヤー構成（z-index 0〜5）で背景・コンテンツ・キャラ・字幕・出典・エンディングを管理しています
- `visual_cue` の3状態（値あり/null/空文字）で自然なコンテンツ遷移を実現しています
- 字幕改行は JIS X 4051 禁則処理 + 均等分割アルゴリズムで、カタカナ語保護や動的フォントスケーリングも実装しています
- フルスクリーンモードは2つの ID 集合（CUE_IDS / LINE_IDS）で柔軟に制御しています
