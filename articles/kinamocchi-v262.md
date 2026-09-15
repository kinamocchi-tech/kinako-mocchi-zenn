---
title: 中国AIがClaudeに勝った？Kimi K3『76%』の数字に潜むベンチマークの罠【解説記事】
emoji: 🤖
type: tech
topics:
- ai
- llm
- tech
published: true
---

<!-- グラレコ:graphreco -->
![中国AIがClaudeに勝った？Kimi K3『76%』の数字に潜むベンチマークの罠【解説記事】｜グラレコ要約](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/V262_graphreco.png)

# 中国AIがClaudeに勝った？Kimi K3『76%』の数字に潜むベンチマークの罠

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [中国AIがClaudeに勝った？Kimi K3『76%』の数字に潜むベンチマークの罠](https://www.youtube.com/watch?v=EVoK68q8ack)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、中国のAIってさ、結局アメリカの猿真似でしょ？
- 🦜 きなこ：今日はね、無料で公開された中国製のAIが、有料の最新Claudeを投票形式のコード対決で打ち負かしたっていう話をするよ
![Title card reveal: "Kimi K3" logo with Chinese flag motif, minimal design](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/005_visual.png)
- 🐹 もっちー：マジで！？その中国AIって何て名前なん！？
- 🐹 もっちー：え、どういうこと！？めっちゃ気になるやん

## Kimi K3って何者？

![Huge glowing number '2.8T' with small caption 'total parameters', dark tech gradient background](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/012_visual.png)
- 🦜 きなこ：じゃあまず、数字を一個だけ言うね。総パラメータ、2.8兆なの
![Bar chart comparing open-weight model parameter counts, one bar towering far above the rest, minimal flat style](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/014_visual.png)
- 🦜 きなこ：桁で言うと2兆8000億。今まで公開された中で、いちばん大きいオープンなモデルなんだよ
![Large block labeled 2.8T with only a small bright slice highlighted and labeled '104B active per token'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/016_visual.png)
- 🦜 きなこ：そこがおもしろいところで、実際に一回の返事で使われるのは、そのうち約1040億だけなの
![Cute flat illustration of a large hospital building with many small doctor icons waiting inside](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/018_visual.png)
- 🦜 きなこ：余ってるんじゃなくて、ちゃんと待機してるの。大きな病院を想像してみて
![Dense grid of 896 tiny doctor icons with only a handful glowing, counter label '896'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/019_visual.png)
- 🦜 きなこ：先生が896人いても、風邪の患者さんに全員は出てこないよね。担当の数人だけが診てくれるの
![Routing diagram: one token arrow entering a router, 16 expert blocks lit plus 2 shared expert blocks](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/021_visual.png)
- 🦜 きなこ：そう。K3は質問ごとに16人を選んで、いつもいる2人を足して動かすんだよ

## Frontend Code Arenaで何が起きたか

![Title card: Frontend Code Arena leaderboard, dark UI with ranking rows](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/031_visual.png)
- 🦜 きなこ：実はこのスペック、まだ何の証明にもなってないの。証明はここから、実際の評価で始まるんだよ
![Simple diagram: browser window with buttons and layout blocks highlighted](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/033_visual.png)
- 🦜 きなこ：落ち着いて。フロントエンドはWebサイトの見た目を作る部分のこと。ボタンとか画面のデザインだね
![Two anonymous code output panels side by side with a vote button](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/035_visual.png)
- 🦜 きなこ：そのとおり。開発者が同じお題をAIに出して、返ってきた画面を見比べて投票していくの
![Blind test icon: two panels labeled A and B with model names blurred out](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/037_visual.png)
- 🦜 きなこ：ううん、そこが一番大事。ブラインド、つまりどのAIの回答かを伏せた状態で投票するんだよ
![Leaderboard rank 1 row highlighted with a gold marker](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/039_visual.png)
- 🦜 きなこ：そう、中身だけで殴り合う土俵なの。そのブラインド投票で、Kimi K3が首位を取ったんだよ
![Bar chart comparing Elo: 1679 vs 1631 vs 1618, top bar emphasized](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/041_visual.png)
- 🦜 きなこ：スコアは1679Elo。2位のClaude Fable 5が1631、3位のGPT-5.6 Solが1618なの

## ベンチマーク解釈の罠

- 🦜 きなこ：その引っかかり、すごく良いところなの。実はその読み方、私も一度は真に受けて、あとで読み違えてたって気づいたの
![Stamp animation: a REFUTED 0-3 seal dropping onto the claim card](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/053_visual.png)
- 🦜 きなこ：そこなんだよ。その読み方ね、今回のリサーチの検証チームが3人全員一致で棄却してるの
![Diagram: 25 extracted claims flowing into three skeptical verifier icons attempting rebuttal](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/055_visual.png)
- 🦜 きなこ：今回のリサーチね、上位25個の主張を3人の懐疑的な検証者が、わざと反証しにかかる仕組みなの
![Tally chart: 25 claims split into 20 confirmed in green and 5 refuted in red](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/057_visual.png)
- 🦜 きなこ：そう。2人以上が反証できたら、その主張は棄却。25個中5個が実際に落とされたんだよ
![List of the five refuted claims, the 76% claim highlighted with a 0-3 vote badge](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/059_visual.png)
- 🦜 きなこ：入ってた。しかも票は0対3。3人とも反証できて、誰ひとり擁護できなかった読み方なの
![Round-robin bracket illustration: one model facing many opponents, average win-rate meter reading 76%](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/061_visual.png)
- 🦜 きなこ：あれはね、全部の対戦相手に対する平均の勝率なの。いろんなモデルと総当たりした打率みたいな数字

## オープンウェイト公開と検証可能性

![A huge glowing model file being downloaded onto a small laptop, flat minimal illustration, arrow from cloud to device](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/073_visual.png)
- 🦜 きなこ：もっちー、あのKimi K3の中身をまるごと自分のパソコンに落とせるって言ったら、信じる？
![Split panel: locked API endpoint on the left, open box with visible internals on the right](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/077_visual.png)
- 🦜 きなこ：個人でだと正直厳しいの。飼い主のタブレット回線だと落とすだけで一生かかりそう。でも誰でも取りに行けるのが大事なんだよ
![Term card revealing the label OPEN-WEIGHT over a package icon containing only model weights](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/079_visual.png)
- 🦜 きなこ：そう。この、重みだけを公開して配る形のことを、オープンウェイトって呼ぶんだよ
![Comparison table: OPEN-WEIGHT vs OPEN-SOURCE, rows for weights, training data, training code, with check and cross marks](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/081_visual.png)
- 🦜 きなこ：そこが違うの。公開されてるのは重みだけで、学習に使ったデータも学習コードも入ってないんだよ
![License document card titled Kimi K3 License with a small asterisk and fine-print lines, flat illustration](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/085_visual.png)
- 🦜 きなこ：そのタダにも条件があるの。Kimi K3ライセンスっていう、独自のライセンスが付いてるんだよ
![License clause diagram: revenue threshold gauge at 20 million dollars per 12 months, branch to separate agreement required](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/087_visual.png)
- 🦜 きなこ：落ち着いて。基本は商用でも使えるの。ただ12か月の収益が2,000万ドルを超えるホスティング事業は、別契約が必要なんだよ

## 専門家の反応と地政学インパクト（慎重に）

![Title card: 'CONFIDENCE LEVEL: LOW' stamped over the section heading, amber warning tone, subtle flicker](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/093_visual.png)
- 🦜 きなこ：実はここ、私も自信を持って言い切れないところなんだよ。だから最初に白状しておくね
![Two-column board appears: left column 'VERIFIED' filled with green check cards, right column 'UNVERIFIED' mostly empty grey slots](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/095_visual.png)
- 🦜 きなこ：専門家がこのモデルをどう見たか、っていう話なんだけど、ちゃんと裏が取れた情報がほとんど無いの
![Info card slides in: name plate with university crest placeholder, a green 'CONFIRMED' badge attached to the job-title row only](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/097_visual.png)
- 🦜 きなこ：流れてはいるんだよ。例えばウォートン校の准教授、イーサン・モリックさんの名前はよく出てくるの
![Same info card splits in two: title row keeps green CONFIRMED badge, quote row gets a large amber 'NEEDS CHECK' label with dashed border](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/098_visual.png)
- 🦜 きなこ：肩書きは大学の公式ページで確認できた。でも、その人が実際に何て言ったかは確認できてないんだよ
![Source-strength ladder diagram: official docs at top (strong), news at middle, social posts at bottom marked with a thin amber bar](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/100_visual.png)
- 🦜 きなこ：そう。SNSの投稿が出典だと、それだけじゃ裏付けとしては弱い、って私は扱ってるの
![Split panel: left 'WHO SAID IT' with a portrait silhouette dimming out, right 'WHERE TO VERIFY' with a document icon lighting up](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/102_visual.png)
- 🦜 きなこ：誰が言ったかより、どこで確認できるか。ここを分けて見るのが、情報の見分け方の第一歩なんだよ

## 実力は本物、でも鵜呑みは禁物

![Replay of the opening hook screen with two question marks fading into checkmarks](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/113_visual.png)
- 🦜 きなこ：じゃあ最初に出した2つの疑問、ここでまとめて答えを出すね
![Small recap badge: Frontend Code Arena rank 1, with a faded strike-through over the misread 76% figure](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/115_visual.png)
- 🦜 きなこ：フロントエンドの部門では正真正銘の1位を取ってるの。さっき確認した通り、あの76%は勘違いだったけどね
![Overall intelligence index ranking chart: Kimi K3 sits in 3rd place behind two US frontier models](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/117_visual.png)
- 🦜 きなこ：そのとおり。総合力を測る指標で見ると3位なの。全部の分野で一番ってわけじゃないんだよね
![Evidence quality meter with three bars: community blind votes / vendor self-reported scores / independent replication (still empty)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/119_visual.png)
- 🦜 きなこ：そう。しかも今の数字は、開発者のブラインド投票と、作った会社自身の自己申告が中心になってて、独立した第三者の再現はまだなの
![Three-state trust gauge: false / unverified / true, pointer resting on the middle zone](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/121_visual.png)
- 🦜 きなこ：ゼロだと決めつけるわけじゃないけど、丸ごと鵜呑みにもしない。それくらいの距離感がちょうどいいの
![Takeaway card with two checkboxes: which category was measured / who measured it](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/126_visual.png)
- 🦜 きなこ：いいね、それが一番大事な見分け方なの。数字そのものより、どんな条件で出た数字なのかを見るんだよ

## まとめ

![Summary slide titled 'Today's Takeaways' with three empty bullet slots](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/129_visual.png)
- 🦜 きなこ：じゃあ最後に、今日わかったことをぎゅっとまとめるね
- 🐹 もっちー：おねがい。ぼく、もう頭ん中がいっぱいなんだよ。整理してほしい
![First bullet fills in: genuine top rank on the Frontend Code Arena leaderboard](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V262/131_visual.png)
- 🦜 きなこ：まず、Kimi K3がFrontend Code Arenaで首位を取ったこと自体は本物なんだよ
- 🐹 もっちー：そこはホンマやったんや！ワイ、疑ってしもてたわ！

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*