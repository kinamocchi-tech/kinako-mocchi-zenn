---
title: "キャラ一貫性の5本柱 ― LOCKED構文でAIにキャラを守らせる"
---

スタンプを 1 枚だけ作るなら、AI 画像生成は十分すぎるほど優秀です。問題は **40 枚を「同じキャラ」として並べたとき**に起こります。1 枚目はメガネをかけているのに、15 枚目では消えている。胴体の色が少しずつくすんでいく。羽の毛束が 3 本から 2 本になる。これがいわゆる **キャラドリフト**です。

LINE スタンプは 40 枚がワンセットで並んで売られます。1 枚でもキャラが崩れていれば、購入者は即座に「雑なセット」と気づきます。そして審査でも「同一キャラクターのセットであること」は事実上の前提です。**一貫性こそがスタンプ制作の最大の技術的ハードル**であり、この章はそれを正面から解決します。

筆者は第 2 弾「きなこ」（セキセイインコ・銀縁メガネ + 薄紫ネッカチーフ）の制作で、この問題を 5 段階の修正を経て克服しました。その過程で確立した **キャラ一貫性の 5 本柱**を、実際のプロンプト断片付きで余すところなく解説します。

:::message
この章は本書の目玉です。ここで紹介する LOCKED 構文と 5 本柱は、`gpt-image-2`（OpenAI の画像生成モデル）を前提にしていますが、考え方はどの画像生成 API でも応用できます。
:::

## なぜ AI はメガネを消すのか ― 簡略化バイアスの正体

まず、敵を正しく理解します。

`gpt-image-2` をはじめとする画像生成モデルは、**「ポーズや構図の自然さ」を「細かいアクセサリーの正確さ」より優先する**という強い傾向を持っています。これをここでは **簡略化バイアス**と呼びます。

具体的にどう現れたか。きなこの制作では、以下のスタンプで銀縁メガネが消失または劣化しました。

| スタンプ | ポーズ | 何が起きたか |
|---------|--------|------------|
| K15 | 正面・合掌（お願い） | メガネが極端に小さくなった |
| K18 | はにかみ | メガネ位置が額から顔へ滑った |
| K35 | おねだり | メガネ消失 |
| K40 | 感謝のお辞儀 | メガネ消失 |

共通点が見えます。すべて **「女性的で穏やかなポーズ」**です。合掌・はにかみ・お辞儀。AI は「優しく内向きなポーズの女性キャラ」を描くとき、画面全体の見栄えを優先し、**額の上に乗った銀縁メガネという「珍しい配置のディテール」を真っ先に切り捨てる**のです。

ここが重要です。きなこのメガネは「顔にかける」のではなく **「額の上にヘアバンドのように乗せている」**という珍しい配置でした。AI の学習データには「メガネは顔にかけるもの」という圧倒的多数の例があります。そのため、ポーズに集中して描画リソースが足りなくなると、AI は「メガネは顔にあるはず」という事前知識に引っ張られて消すか、顔へずらしてしまうのです。

:::message alert
珍しい配置・珍しいアクセサリーほど簡略化バイアスに負けやすい。「ありふれていない特徴」を持つキャラほど、一貫性確保の難易度が跳ね上がります。
:::

### LoRA という王道と、その現実的な壁

「ならば LoRA でキャラを学習させればいい」という声が当然出ます。実際、専用モデルを学習させる **LoRA + PuLID + ControlNet**（ComfyUI 環境）はキャラ一貫性において最高の品質を出せます。

しかし副業でスタンプを量産する立場では、学習データ準備・GPU 環境構築・運用コストが重くのしかかります。1 キャラごとに学習を回し、ハイパーパラメータを調整し、ComfyUI のワークフローを保守する ― これは「スタンプを売る」という目的に対して明らかにオーバースペックです。

そこで本書が取る現実解はこうです。

> **`gpt-image-2` 単体ではキャラ一貫性が LoRA に劣る。だからこそ、プロンプト工学で徹底的に補完する。**

API を叩くだけで完結し、学習も GPU も不要。その代わり、プロンプトに「AI にキャラを守らせる仕掛け」を全力で仕込む。それが次に解説する 5 本柱です。

## キャラ一貫性の5本柱

5 本柱は独立した小技ではなく、**一つの構造化プロンプトを構成する 5 つの層**です。順に積み上げることで、簡略化バイアスを多層的に押さえ込みます。

### 第1柱: LOCKED 構文 ― 必着属性を宣言する

最も効果が大きく、最初に導入すべきなのが **LOCKED 構文**です。

AI に「このキャラには絶対に消してはいけない属性がある」と明示的に宣言します。コミュニティでの実証でも、`LOCKED:` というプレフィックスで必着属性を箇条書き列挙すると一貫性が顕著に向上することが確認されています。

セクション名は **`LOCKED Attributes — must appear in EVERY output`**（すべての出力に必ず現れる属性）とします。「every output」という強い言い回しがポイントです。

```text
LOCKED Attributes — must appear in EVERY output:
- LOCKED: silver round wire-frame glasses RESTING on forehead (above eyes, NOT on face)
- LOCKED: 3 orange crest feather tufts on crown
- LOCKED: lemon yellow body color (#FAEB79)
- LOCKED: light lavender purple neckerchief, solid color, tied at chest
```

各行のポイントを分解します。

- **メガネ**: 単に「glasses」ではなく `RESTING on forehead (above eyes, NOT on face)` と**配置まで明記**します。珍しい配置こそ言語化が必須です。
- **羽の毛束**: `3 orange crest feather tufts` と**数を数字で固定**します。「いくつか」では AI が勝手に増減させます。
- **胴体の色**: `lemon yellow body color (#FAEB79)` と**カラーコードを併記**します。色名だけだとドリフトで徐々にくすみます。
- **ネッカチーフ**: `solid color, tied at chest` と**色のベタ塗り・結び位置**を指定します。

:::message
LOCKED 行に書くのは「キャラの同一性を決定づける要素」だけに絞ります。背景の小物や毎回変わる表情まで LOCKED に入れると、本当に守るべき属性の重みが薄まります。
:::

### 第2柱: Change vs Preserve 二項対立 ― 変える/変えないを分離する

LOCKED で「守る属性」を宣言したら、次は **「何を変えてよくて、何を絶対に変えてはいけないか」を二項対立で明示**します。これは OpenAI 公式の Cookbook でも推奨されている手法です。

```text
Change ONLY: pose, expression, facing direction
Preserve EXACTLY: glasses position, crest feathers, body color, neckerchief, beak shape, eye style
```

なぜこれが効くのか。AI に「画像を編集して」と指示すると、AI は「どこをどう変えていいのか」の境界が曖昧なまま全体を再解釈します。その結果、変えるべきでない部分（メガネ・色）まで「ついでに」いじってしまう。

`Change ONLY:`（変えるのはこれだけ）と `Preserve EXACTLY:`（これは寸分違わず保持）を明示することで、AI の自由度を**ポーズ・表情・向きの 3 つだけ**に閉じ込めます。残りはすべて「触るな」と宣言するわけです。

ここで `Preserve EXACTLY:` に列挙する項目は、LOCKED 構文で宣言した属性とほぼ重なります。**2 つの柱が互いを補強する**設計になっている点に注目してください。

### 第3柱: 役割ラベル明示 ― どれが本物の参照かを教える

`gpt-image-2` の multi-image edit（複数参照画像を渡す編集）では、**複数のリファレンス画像の「役割」を明示しないと、AI が「どれがキャラ参照なのか」を推測で決めてしまう**という落とし穴があります。

推測に任せると、参照画像の重みが分散し、結果としてどれにも似ない「平均化されたキャラ」が生成されます。これを防ぐため、各画像に役割ラベルを与えます。

```text
Image 1: MASTER reference (kinako character anchor — preserve identity from this)
Image 2-N: SISTER references (additional pose/angle variants of the SAME character)
```

- **MASTER（マスター）**: アイデンティティの錨（anchor）。「このキャラはこの顔だ」という基準を担う 1 枚。
- **SISTER（シスター）**: 同一キャラの別ポーズ・別アングルのバリエーション。マスターを補強する役。

`Image 1` を必ず MASTER に固定するのも公式の推奨です。先頭の画像を identity anchor として優先する挙動があるため、**最も大事な 1 枚を先頭に置く**ことで効果が最大化します。

### 第4柱: CRITICAL ACCESSORY 強制再描画 ― 「描けないなら描き直せ」と命じる

ここが、メガネ消失問題に対する直接の特効薬です。

LOCKED・Change/Preserve・役割ラベルを揃えても、「額のメガネ」のような珍しい配置は依然として簡略化バイアスに負けることがあります。そこで、最後の砦として **強制再描画指示**を追加します。

```text
CRITICAL ACCESSORY (never omit):
The character ALWAYS wears silver round glasses pushed up on her forehead.
The glasses sit ABOVE the eyes, on the feathered forehead, like a headband.
Do NOT draw glasses on the face. Do NOT omit the glasses.
If you cannot fit glasses, redraw — glasses are mandatory.
```

このブロックの設計思想を一行ずつ読み解きます。

- `The character ALWAYS wears...` ― 例外なく常に着用すると断言。
- `like a headband` ― AI が知っている既知の概念（ヘアバンド）に例えて、珍しい配置を理解させる。
- `Do NOT draw glasses on the face. Do NOT omit the glasses.` ― **「顔にかける」「省く」という 2 つの典型的失敗を名指しで禁止**。
- `If you cannot fit glasses, redraw — glasses are mandatory.` ― 決定打。**「メガネが入らないなら、メガネを諦めるのではなく構図ごと描き直せ。メガネは必須だ」**と、AI が逃げる余地を塞ぎます。

簡略化バイアスの本質は「描画が苦しくなったときアクセサリーを切り捨てる」ことです。`If you cannot fit X, redraw` は、その切り捨ての選択肢そのものを禁止する命令なのです。

:::message
この `If you cannot fit X, redraw` の言い回しは、メガネに限らず「珍しい配置のアクセサリーすべて」に転用できます。額の宝石、肩に乗った小動物、特殊な髪型 ― キャラの個性が「珍しさ」にあるほど、この柱が効きます。
:::

### 第5柱: ネガティブプロンプト強化 ― 失敗を具体名詞で禁止する

最後に、**起こってほしくない失敗を具体的な名詞で列挙**します。抽象的な「don't break the character」では弱く、**実際に起きた失敗を固有名詞で名指し**するのが鉄則です。

```text
NEGATIVE: missing glasses, glasses on eyes/face, bare forehead, missing crest feathers,
faded body color, untied neckerchief, redesigned character, extra accessories
```

リストを失敗事例と対応させて読むと、設計意図がわかります。

| ネガティブ語 | 防ぎたい実際の失敗 |
|------------|------------------|
| `missing glasses` | K35/K40 のメガネ消失 |
| `glasses on eyes/face` | K18 の「顔へ滑る」現象 |
| `bare forehead` | メガネが消えて額が剥き出しになる |
| `missing crest feathers` | 羽の毛束の欠落 |
| `faded body color` | 胴体色のドリフト・くすみ |
| `untied neckerchief` | ネッカチーフのほどけ |
| `redesigned character` | キャラ全体の作り直し |
| `extra accessories` | 勝手な小物の追加 |

ネガティブプロンプトは「事後に発見した失敗を、次の生成で潰す」ためのフィードバックループの出口です。新しい失敗パターンを見つけたら、迷わずこのリストに具体名詞を追加していきます。

## リファレンス画像の最適化 ― 3〜5枚・白背景・最明瞭なマスター

5 本柱はプロンプト側の工夫ですが、**渡すリファレンス画像の質と量**も一貫性を大きく左右します。実証データに基づく最適解は次の通りです。

| 観点 | 推奨 | 根拠 |
|------|------|------|
| 枚数 | **3〜5 枚**（master 1 + sister 2〜4） | 10 枚を超えると識別ノイズが増え処理が複雑化する |
| 順序 | **Image 1 = master 固定** | 先頭画像を identity anchor として優先する公式挙動 |
| 形式 | **白背景 RGB 推奨** | 透過 PNG は API エラーの要因になりやすい |
| 選定基準 | **必着要素が最も明瞭に映る 1 枚を master へ** | master の品質が他カットの品質を決定づける |

3 つのポイントを補足します。

**枚数は「多ければ良い」ではない。** 当初きなこの制作では参照画像を 9 枚渡していましたが、3〜5 枚に削減したことで一貫性が向上しました。参照が多すぎると AI が「平均」を取ろうとし、かえってマスターの特徴が薄まります。**master 1 枚 + sister 2〜4 枚**が黄金比です。

**透過 PNG を参照に使わない。** 後の章で背景透過を詳しく扱いますが、リファレンスとして渡す画像は**白背景の RGB**にしてください。透過 PNG（RGBA）はリファレンスとして渡すと API エラーを起こしやすく、安定生成の妨げになります。

**master 選びがすべてを決める。** master には「メガネ・羽の毛束・ネッカチーフがすべて最も明瞭に映っている 1 枚」を選びます。master がぼやけていたり、肝心のメガネが半分隠れていたりすると、そこを起点に全カットの品質が落ちます。

:::message
3 章で作ったキャラクターシートが、ここで生きます。シートの中で「正解の顔・正解のアクセサリー配置」が最も鮮明に描けたカットを master に採用してください。
:::

## 構造化プロンプトテンプレート ― 6セクションを組み立てる

5 本柱とリファレンス最適化を 1 つのプロンプトに統合します。実際のコードでは、6 つのセクションを連結する組み立て関数として実装しています。

```python
def assemble_v2_prompt(base, spec, char_name, locked_attrs, master_path, sister_paths):
    return f"""
[Reference Images]
Image 1: MASTER anchor — preserve {char_name}'s identity from this image.
Images 2-{len(sister_paths)+1}: SISTER references — same character, different poses/angles.

[Subject]
{base}
Pose: {spec.pose}
Expression: {spec.expression}
Facing: {spec.facing}

[LOCKED Attributes — must appear in EVERY output]
{format_locked_list(locked_attrs)}

[Change vs Preserve]
Change ONLY: pose, expression, facing direction
Preserve EXACTLY: {", ".join(locked_attrs)}

[Style]
Manga-style finish with thick clean dark-brown ink outline,
flat pastel cell-shaded coloring, soft anime sticker aesthetic.
1024x1024 white background.

[Constraints / Negative]
NEGATIVE: missing locked attributes, redesigned character, photorealistic,
multiple characters, watermark, extra limbs, asymmetric eyes
"""
```

6 セクションの役割を整理します。

| セクション | 担当する柱 | 役割 |
|-----------|-----------|------|
| `[Reference Images]` | 第3柱 | master/sister の役割ラベルを宣言 |
| `[Subject]` | ― | 今回だけ変える要素（pose/expression/facing）を指定 |
| `[LOCKED Attributes]` | 第1柱 | 必着属性を列挙 |
| `[Change vs Preserve]` | 第2柱 | 変える/守るを二項対立で分離 |
| `[Style]` | ― | 画風（太い濃茶インク輪郭・パステルセル塗り）を固定 |
| `[Constraints / Negative]` | 第5柱 | 具体名詞で失敗を禁止 |

第4柱（CRITICAL ACCESSORY）は、**珍しい配置のアクセサリーを持つキャラのときだけ** `[Subject]` の直後に挿入します。きなこのメガネのようなケースで追加する「条件付きの第 6 セクション」と捉えてください。

:::details なぜセクションをラベルで囲うのか
`[LOCKED Attributes]` のように角括弧つきの見出しでブロックを区切ると、AI がプロンプトを「指示の塊」として構造的に解釈しやすくなります。だらだらと 1 段落で書くと、後半の指示ほど無視されやすくなります。**重要な制約ほど独立したラベル付きブロックに切り出す**のがコツです。
:::

## 業界比較 ― gpt-image-2 + 本ガイドはどこに位置するのか

ここまでの工夫が、ツール選択の地図の中でどこに位置するのかを示します。2026 年時点の主要ツールのキャラ一貫性を比較します。

| ツール | キャラ一貫性 | 特徴 |
|------|-----------|------|
| LoRA + PuLID + ControlNet（ComfyUI） | ★★★★★ | 最高品質。ただし学習・GPU・運用コストが高い |
| Midjourney `--cref` / `--sref` | ★★★★ | キャラ参照機能が成熟。API 連携は弱め |
| **gpt-image-2 + 本ガイド** | **★★★** | **プロンプト工学で補完。API で完結し量産向き** |
| DALL-E 3 / Adobe Firefly | ★★ | キャラ再現は弱め |

正直に書きます。**`gpt-image-2` は単体ではキャラ一貫性で LoRA に劣ります**（★★★ 対 ★★★★★）。素のままなら DALL-E 3 と大差ない領域に落ちることもあります。

しかし本ガイドの 5 本柱を適用すると、★★ の素材を **★★★ の実用ラインへ引き上げられます**。そして ★★★ は「40 枚のスタンプセットを審査通過させ、購入者が同一キャラと認識する」には十分な水準です。学習も GPU も不要で、API を叩くだけ。**量産の現場で回し続けられる**という一点で、本書はこの選択を推します。

## 失敗パターン早見表 ― 症状から対策を引く

最後に、実制作で遭遇した失敗を「症状 → 原因 → 対策」で一覧化します。新しいキャラで一貫性が崩れたら、まずこの表を引いてください。

| 症状 | 原因 | 対策 |
|------|------|------|
| 女性的ポーズ（合掌・はにかみ）でメガネ消失 | 「ポーズの自然さ > アクセサリー」の簡略化バイアス | LOCKED + そのカット個別に `Even in this gentle pose, glasses remain visible` を追記。ポーズを `celebratory jump` 等の動きのある構図へ変更 |
| 全体の見栄え優先で細部が省かれる | モデルの簡略化バイアス | LOCKED 構文 + 第4柱 `If you cannot fit X, redraw` |
| sister が多すぎて master に似ない | 参照画像の重みが分散 | リファレンスを 3〜5 枚に削減し master を先頭固定 |
| 透過 PNG リファレンスで API エラー | API 仕様（RGBA 参照は不安定） | 白背景 RGB に統一 |
| 胴体の色が枚を追うごとにくすむ | カラーコード未指定によるドリフト | LOCKED に `(#FAEB79)` のようにカラーコードを併記 |
| 羽の毛束の本数が増減する | 数量の言語化漏れ | `3 crest feather tufts` と数字で固定 |

特に 1 行目の「女性的ポーズでメガネ消失」は、きなこ K15 で実際に起きた現象です。最終的にポーズを正面合掌から **celebratory jump（祝福のジャンプ）**へ変更し、メガネ強調の文言を足すことで解決しました。**「プロンプトで守りきれないなら、そもそも簡略化を誘発するポーズを避ける」**という構図設計の判断も、一貫性を守る立派な一手です。

## この章のまとめ

- `gpt-image-2` には **簡略化バイアス**があり、ポーズの自然さを優先して額のメガネ等「珍しい配置のアクセサリー」を消失させる（きなこ K15/K18/K35/K40 で実際に発生）。単体ではキャラ一貫性が LoRA に劣るため、**プロンプト工学で補完するのが現実解**である。
- **キャラ一貫性の 5 本柱**は、①LOCKED 構文（必着属性を宣言）②Change vs Preserve（変える/守るを分離）③役割ラベル（master/sister）④CRITICAL ACCESSORY（`If you cannot fit X, redraw` で強制再描画）⑤ネガティブ強化（失敗を具体名詞で禁止）であり、1 つの構造化プロンプトを多層で構成する。
- リファレンスは **3〜5 枚・白背景 RGB・必着要素が最も明瞭な 1 枚を master に先頭固定**するのが最適。透過 PNG は API エラーの要因になるため使わない。
- プロンプトは **6 セクション（Reference / Subject / LOCKED / Change-Preserve / Style / Negative）**のラベル付きブロックで組み立て、重要な制約ほど独立ブロックに切り出す。
- 業界比較では本ガイドの `gpt-image-2` は **★★★**（LoRA は ★★★★★）だが、API 完結・学習不要で量産現場を回せる点が決定的な強みである。

5 本柱を 1 枚に適用できるようになったら、次はそれを **40 枚に展開する**段階です。しかしここで新たな敵が現れます ― 枚数が増えるほど、体型・色・線が少しずつズレていく**キャラドリフト**です。次章では、40 個の量産を「チェックポイント方式」で乗り切り、ドリフトを検知して再キャリブレーションする具体的な運用を解説します。
