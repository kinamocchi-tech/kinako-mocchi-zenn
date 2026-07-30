---
title: JSONが壊れない！Claude APIの新機能3つがAI開発を変える理由【解説記事】
emoji: 🤖
type: tech
topics:
- voicevox
- ai
- compaction
- claude
- llm
published: true
---

# JSONが壊れない！Claude APIの新機能3つがAI開発を変える理由

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [JSONが壊れない！Claude APIの新機能3つがAI開発を変える理由](https://youtu.be/QEmwKPBxoQs)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、APIにJSON返してって言ったのに、壊れたデータが返ってきたことない？
- 🐹 もっちー：おお！全部解決してくれるの？めっちゃ気になる！

## 開発者が抱えていた3つの悩み

![「従来のClaude APIが抱えていた3つの課題」を見出しで表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/007.png)
- 🦜 きなこ：まず、3つの機能がどんな課題を解決するのか整理しようね
- 🦜 きなこ：1つ目は、JSON出力の不安定さ
- 🦜 きなこ：AIにJSONで返してって頼んでも、たまに形式が崩れてシステムがクラッシュしちゃうの
![ダミーツールによるJSONハックの流れ図（tool_choice→強制的にJSON化→でも不安定）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/011.png)
- 🦜 きなこ：まさにそんな感じ。JSONで返してって指定しても、閉じカッコが抜けたり余計なテキストが混ざったり
![ダミーツールによるJSONハックの流れ図（tool_choice→強制的にJSON化→でも不安定）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/011b.png)
- 🦜 きなこ：だから開発者はダミーのツールを定義して、無理やりJSON形式にするハックを使ってたの
- 🦜 きなこ：実際、多くの開発者がリトライロジックとかエラーハンドリングに時間を取られてたの

## Structured Outputs — JSON出力を100%保証

![「Structured Outputs」のタイトルカード。JSON Schemaのアイコンとチェックマーク](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/020.png)
- 🦜 きなこ：じゃあ1つ目の機能、Structured Outputsから見ていこう
- 🦜 きなこ：これは、AIの出力を100%指定したJSON形式に従わせる機能だよ
![制約付きデコーディングの仕組み図：JSON Schema → グラマーにコンパイル → トークン生成時に制約適用](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/023.png)
- 🦜 きなこ：仕組みが面白いの。制約付きデコーディングっていう技術を使ってるんだけどね
- 🦜 きなこ：開発者が定義したJSON Schemaを、内部でグラマーにコンパイルするの
- 🦜 きなこ：そのグラマーに違反するトークンは、物理的に生成できないようにブロックされるの
- 🦜 きなこ：そう、だからスキーマ違反は原理的に起きないの

## Compaction — 無限の会話を実現

![「Compaction API」のタイトルカード。圧縮のアイコンと無限大マーク](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/035.png)
- 🦜 きなこ：2つ目の機能はCompaction。コンテキストの自動圧縮機能だよ
![コンテキストウィンドウの概念図：会話が積み重なってウィンドウが埋まっていくイメージ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/037.png)
- 🦜 きなこ：そう。会話が長くなると、過去のやり取りがどんどん溜まるでしょ？
- 🦜 きなこ：Compactionは、溜まった会話を自動で要約して圧縮してくれるの
![Compactionの発動フロー図：入力トークン数が閾値（150,000）を超過 → 自動要約 → 圧縮されたコンテキストで継続](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/040.png)
- 🦜 きなこ：いい例えだね。仕組みとしては、入力トークンが閾値を超えると自動で発動するの
- 🦜 きなこ：デフォルトの閾値は15万トークン。最小で5万トークンから設定できるよ
![トークン削減の効果グラフ：圧縮前vs圧縮後、約58%削減](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/043.png)
- 🦜 きなこ：サードパーティの検証では、約58%のトークン削減が報告されているよ

## Adaptive Thinking — AIが考える深さを自分で決める

![「Adaptive Thinking」のタイトルカード。脳のアイコンとレベルメーター](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/051.png)
- 🦜 きなこ：3つ目はAdaptive Thinking。推論の深さを動的に調整する機能だよ
![従来のExtended Thinking図：開発者が手動でbudget_tokens=10000を設定 → 全リクエストに一律適用](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/053.png)
- 🦜 きなこ：以前のExtended Thinkingでは、思考にかけるトークン予算を開発者が手動で設定してたの
- 🦜 きなこ：Adaptive Thinkingでは、AIが問題の難しさを自分で判断して、思考量を自動調整するの
![effortパラメータ4段階比較表：max（Opus専用・制限なし）、high（デフォルト・深い推論）、medium（バランス）、low（速度重視）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/056.png)
- 🦜 きなこ：開発者はeffortパラメータで4段階のガイダンスを与えられるよ
- 🦜 きなこ：maxはOpus 4.6専用で思考に制限なし。highがデフォルトだよ
- 🦜 きなこ：いい質問。effortはソフトシグナルだから、lowでも複雑な問題なら思考するの

## Anthropicの戦略とリリースタイムライン

![2026年Q1 リリースタイムライン図：1/29 Structured Outputs GA → 2/5 Opus 4.6+Adaptive Thinking+Compaction(β) → 2/17 Sonnet 4.6 → 2/19 Memory+Auto Caching → 3月 1M Context GA](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/069.png)
- 🦜 きなこ：ここで、この3機能のリリースタイムラインを振り返ってみよう
- 🦜 きなこ：1月29日にStructured Outputsが一般提供になって、APIの型安全性がまず確保されたの
- 🦜 きなこ：2月5日にOpus 4.6と一緒に、Adaptive ThinkingとCompactionが同時に投入されたの
- 🦜 きなこ：2月17日にはSonnet 4.6がリリースされて、コスパの良い選択肢も用意されたよ
- 🦜 きなこ：そう。budget_tokensの手動設定は今後削除予定って公式に予告されてるの
- 🦜 きなこ：さらに2月19日にMemory ToolとAuto Cachingが一般提供になって、3月には1Mコンテキストも正式リリース

## 開発者コミュニティの反応と組み合わせパターン

![「開発者コミュニティの声」タイトルカード。HN・Reddit・日本の開発者コミュニティのロゴ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/078.png)
- 🦜 きなこ：開発者コミュニティの反応も見てみよう
- 🦜 きなこ：Structured OutputsはHacker Newsで184ポイントを獲得したよ
![HNコメントの引用表示：「LLM自動化の根幹なのに今まで無かったのが異常」「OpenAIへのキャッチアップ」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/080.png)
- 🦜 きなこ：「LLM自動化の根幹なのに今まで無かったのが異常」という声が多かったの
- 🦜 きなこ：日本の開発者からは、MarkdownをJSON出力に含めるとパースエラーになるケースが報告されてるよ
- 🦜 きなこ：Compactionについては「OpenAIに同等機能がない」と、Anthropic独自の競争優位として評価されてるよ
![CADDiの運用指針図：70%以下=Smart Zone（品質安定）、70-100%=Risk Zone（品質劣化リスク）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/083.png)
- 🦜 きなこ：日本の製造業プラットフォームCADDiは、コンテキスト使用率70%以下を維持する運用指針を公開してるの

## まとめ

![まとめカード「Claude API 3大新機能」：1. Structured Outputs — JSON出力を100%保証 2. Compaction — コンテキスト自動圧縮 3. Adaptive Thinking — 思考の深さを動的調整](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V015/090.png)
- 🦜 きなこ：今日のまとめをしようか
- 🦜 きなこ：Structured OutputsでJSON出力が100%保証されるようになった
- 🦜 きなこ：Compactionで長時間の会話もコンテキストを圧縮して継続できるようになった
- 🦜 きなこ：Adaptive ThinkingでAIが問題の難しさに応じて思考量を自動調整するようになった

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*