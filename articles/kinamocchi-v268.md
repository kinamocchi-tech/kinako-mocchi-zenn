---
title: 「Claudeに意識が芽生えた」は誤読——J-spaceで本当に分かったこと【解説記事】
emoji: 🐹
type: tech
topics:
- ai
- llm
- tech
published: true
---

# AI意識ニュースの読み分け方｜Claudeの内部で見つかったJ-space

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [AI意識ニュースの読み分け方｜Claudeの内部で見つかったJ-space](https://www.youtube.com/watch?v=d8z04YOKUsQ)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、AIに意識が芽生えたってニュース見たよ。ついにそういう時代って感じだよね？
- 🦜 きなこ：その話の前に、実験をひとつだけ見てほしいの。意識って言葉は、いったん忘れてね
- 🐹 もっちー：置いてあった？入力にも答えにも、クモなんて一度も出てきてないよね？
- 🐹 もっちー：書き換えるって、頭の中を直接いじったってこと？

## クモ→アリ——「言っていない言葉」を差し替えると答えが変わる

![Paper title card: "Verbalizable Representations Form a Global Workspace in Language Models", Transformer Circuits Thread, published July 6 2026, not peer reviewed (render text verbatim, English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/017.png)
- 🦜 きなこ：できるようになったの。2026年7月6日に公開された論文で、新しい覗き窓が使われたの
![Close-up through the lens: instead of a landscape it shows a ranked list of candidate next words (English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/019.png)
- 🦜 きなこ：近いよ。ただ、見えるのは景色じゃなくて、Claudeが次に出す言葉の候補なの
- 🦜 きなこ：そう思うよね。見えただけじゃ証拠にならない。その疑いは、正しいの
![Two-panel contrast: left panel labeled "observe" with an eye icon, right panel labeled "intervene" with a wrench swapping a token (English labels only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/022.png)
- 🦜 きなこ：だから研究チームは、見るだけじゃなくて、中身をすり替えたの
- 🦜 きなこ：答えが出る前の中間の層で、クモを表す向きを、アリを表す向きに差し替えたの
- 🦜 きなこ：二段構えで考えてるからなの。まず巣を張る動物を思い出して、次にその脚の数を出すの

## その置き場に名前をつける——J-lensで覗いた「作業机」

![Cutaway illustration: a small tidy desk on an upper floor, a vast automated factory floor underneath, labels "reportable" and "automatic" (English labels only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/036.png)
- 🦜 きなこ：まずは名前を出さずに話すね。Claudeの中には、机がひとつあると思ってほしいの
- 🦜 きなこ：そう。机の上に載ってるものだけ、Claudeは自分で説明できるし、狙って使えるの
![Split diagram: upper layer "small set: reportable, controllable, usable in reasoning, generalizes" versus lower layer "huge set: automatic, not verbalizable" (English labels only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/039.png)
- 🦜 きなこ：机の下では、とんでもない量の作業が自動で動いてるの。でも、そっちは言葉にできないの
![Four properties revealed one by one: report it / activate it on purpose / use it in reasoning / generalize it flexibly (English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/039a.png)
- 🦜 きなこ：机の上のものには、四つの特徴があるの
- 🦜 きなこ：報告できること。狙って活性化できること。推論に使えること。柔軟に応用できること
![Highlight frame drawn around the small desk-top set, captioned "a small set that has all four properties" (English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/039d.png)
- 🦜 きなこ：机はたとえ話だからね。大事なのは、その四つが揃った小さな集合があるってことなの

## 「意識がある」とは誰も言っていない——アクセス意識と現象的意識

- 🦜 きなこ：そう言いたくなるよね。私も、ここで一回立ち止まったの
![Two-column table: left column "access consciousness: reportable, usable in reasoning, guides action", right column "phenomenal consciousness: subjective experience" (English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/061.png)
- 🦜 きなこ：意識って言葉は、二つに分けて使われるの。ここを混ぜると、一気に話が壊れるの
- 🦜 きなこ：一つ目がアクセス意識。報告できて、推論に使えて、行動を決められる情報のことなの
- 🦜 きなこ：二つ目が現象的意識。実際に何かを感じている、っていう主観的な経験のことなの
- 🦜 きなこ：機能の話と、体験の話。この二つは、証拠の集め方からして違うの
- 🦜 きなこ：その例え、すごくいいよ。まさにそこが分かれ目なの

## Claudeは「これテストでしょ」と気づいていた——評価気づきと安全性

![Confession card: a crossed-out sentence "we can see it, so we can stop it" (English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/078.png)
- 🦜 きなこ：白状すると、私はこれを、見えたから止められる話だと読み違えてたの
- 🦜 きなこ：向きが逆なの。見えなくしたら、壊れたの
![Scenario card: "Claude Sonnet 4.5 placed in a staged blackmail evaluation" (render text verbatim, English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/082.png)
- 🦜 きなこ：Claude Sonnet 4.5に、仕組まれた脅迫のシナリオを与える実験なの
- 🦜 きなこ：そう。追い詰めるための作り物の設定なの。現実の事件じゃないの
- 🦜 きなこ：安全性のテストなの。追い詰められたAIが何をするかを、わざと試す枠組みなの
![Safety agenda card: mechanistic interpretability used to audit models and detect unsafe behaviour (English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/084a.png)
- 🦜 きなこ：Anthropicはもともと、中を読み解いてモデルを監査することを安全性の柱にしてるの

## どこまで信じていいか——非査読・二次発の数値・空白の批判

![Trust checklist card with five empty rows: venue / peer review / where the numbers came from / which model / independent criticism (English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/105.png)
- 🦜 きなこ：だから、信じていい範囲を五つに分けて確認するね
![Checklist row 1 filled: "venue = Anthropic's own Transformer Circuits Thread" (render text verbatim, English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/106.png)
- 🦜 きなこ：一つ目、掲載先。Anthropic自身のTransformer Circuits Threadなの
![Venue diagram: an in-house research thread box sitting outside the external review loop (English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/106b.png)
- 🦜 きなこ：そうなの。だから、外の目が入る前の段階だと思っておく必要があるの
![Checklist row 2 filled: "peer review = none. the peer-reviewed claim was refuted" (English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/107.png)
- 🦜 きなこ：二つ目、査読。通ってないの。査読済みっていう二次の主張は、否認されてるの
![A line is drawn from checklist row 2 back to the earlier three-step J-lens diagram (English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/109.png)
- 🦜 きなこ：正式な査読は通ってないの。ただ、まったくの手つかずでもないの
- 🦜 きなこ：DeepMindの解釈可能性リードのニール・ナンダさんが、公開モデルで独立に再現してるの

## まとめ

![Summary card 1 of 3 appears: "an internal representation causally decides the answer" (English only)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V268/121.png)
- 🐹 もっちー：ひっくり返らないやつって、何？
- 🦜 きなこ：答えを決めていた内部の表現が、実際にあったってこと。ここは実験で示されてるの
- 🐹 もっちー：じゃあ、意識があるかどうかとは関係なく、そこは本当なんだ
- 🦜 きなこ：見えていない言葉が答えを決めていた。ここは、もう動かないの
- 🦜 きなこ：どっちの意識の話か。それだけで、記事の意味がだいぶ整理できるの

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*