---
title: Anthropicが『提訴』しなかった理由——Alibaba2,880万件不正利用の真相【解説記事】
emoji: 🐹
type: tech
topics:
- ai
- llm
- tech
published: true
---

# Anthropicが『提訴』しなかった理由——Alibaba2,880万件不正利用の真相

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [Anthropicが『提訴』しなかった理由——Alibaba2,880万件不正利用の真相](https://www.youtube.com/watch?v=lr91GPWfKLo)
:::

## この記事で分かること

- 🐹 もっちー：なあきなこ、こないだニュースで見たんやけど、Anthropicが中国のAlibaba系のAI企業を提訴したんやろ？
- 🐹 もっちー：え！？提訴されたって記事で見た気がするんだけど…
- 🐹 もっちー：手紙…？裁判起こすほどのことじゃなかったってこと？
- 🐹 もっちー：そんな大事件やのに、なんで訴えへんかったん！？

## 何が起きたか — 2つの事案の混同を解く

![2つの事案を比較する表（時期・企業・規模）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/012.png)
- 🦜 きなこ：実はね、この話には似てるけど別の事案が2つあるの。まずそこを整理させて
- 🦜 きなこ：1つ目は2026年2月、AnthropicがDeepSeekやMoonshot AIなど中国3社を公式ブログで名指しした事案なの
- 🦜 きなこ：2つ目が今日の主役。2026年6月、Alibaba傘下のQwenラボを対象にした、また別の事案なんだよ
![数値のカウントアップ演出](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/017.png)
- 🦜 きなこ：期間は2026年4月22日から6月5日までの44日間。この間に約2万5千件の偽アカウントが使われたの
- 🦜 きなこ：そのアカウントを使って、Claudeとのやり取りが2,880万件を超えたの。これがAnthropicの主張なんだよ
- 🦜 きなこ：その例え、なるほどって思ったよ（笑）

## 手口の解説 — 敵対的蒸留とは何か

![敵対的蒸留（Adversarial Distillation）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/029.png)
- 🦜 きなこ：この手口には名前がついてて、『敵対的蒸留』って呼ばれてるの
![STEP1: 偽アカウントでブラックボックスAPIアクセスを取得](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/031.png)
- 🦜 きなこ：イメージとしては近いよ。手順は3つ。まず偽アカウントでAPIに侵入するの
![STEP2: 大量プロンプトで推論パターンを抽出](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/032.png)
- 🦜 きなこ：次に、工夫したプロンプトを大量に投げて、Claudeの考え方のクセを抜き取るの
- 🦜 きなこ：まさにそんなイメージだね。ひたすら繰り返して、少しずつデータを集めていくの
![STEP3: 入出力ペアで競合モデルを訓練](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/033.png)
- 🦜 きなこ：最後に、その入出力のペアを使って、自分たちの競合モデルを鍛え直すの
- 🦜 きなこ：すごく的を射た例えだね。まさにそういうこと

## Anthropicの検知方法 — なぜ見抜けたのか

- 🦜 きなこ：それがね、中身を読んで見つけたわけじゃないの。実はそこが、この話の面白いところなんだよ
- 🦜 きなこ：順番に説明するね。まず大前提として、蒸留の質問は一件だけ見ても普通の利用と区別がつかないの
![2,880万回の会話＝2,880万人の普通ユーザーに見える](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/061.png)
- 🦜 きなこ：そう。2,880万回のやり取りも、一件ずつ見れば2,880万人の好奇心旺盛なユーザーに見えちゃうの
![Diagram: the deciding factor is not "content" but "behavioral signals"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/063.png)
- 🦜 きなこ：だからAnthropicは、中身じゃなくて『行動のパターン』で見抜いたの
- 🦜 きなこ：簡単に言うとね、一件ずつじゃなくて、たくさんのアカウントの動き方をまとめて観察するの
![検知シグナル①複数アカウントの協調 ②IP・プロキシ相関](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/067.png)
- 🦜 きなこ：その例え、いいね。複数アカウントが連携してる動きや、接続元の相関を手がかりにするんだよ

## 法的構成 — なぜ訴訟ではなく書簡なのか

![Caption: "Van Buren ruling, June 2021"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/077.png)
- 🦜 きなこ：そこには背景があってね、2021年に出たある最高裁判決のせいで、実はけっこう微妙な話になってるんだよ
![テロップ「CFAA = Computer Fraud and Abuse Act」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/079.png)
- 🦜 きなこ：Van Buren対アメリカ合衆国っていう判決。CFAA、コンピュータ詐欺乱用法の解釈を決めた重要な判例なの
- 🦜 きなこ：正式には18 U.S.C. § 1030。アメリカでハッキングや不正アクセスを取り締まる連邦法だよ
![Caption: "Decided 6-3"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/083.png)
- 🦜 きなこ：2021年6月、最高裁は6対3で「認可されたアクセスを超える」の意味をすごく狭く解釈したの
![Diagram: "Gate open/close metaphor"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/085.png)
- 🦜 きなこ：門が開いてるか閉じてるか、それだけで判断するの。開いてる門から入ったなら、中で何しても違反にならないって考え方
![Diagram: "Fake accounts still count as valid accounts"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/087.png)
- 🦜 きなこ：そう。Qwenの偽アカウントも、Claudeから見れば「有効なアカウント」として作られてた。門は開いてたの

## 開発者への教訓 — 合法的API利用チェックリスト

- 🦜 きなこ：ここからは、検知シグナルの裏返しとして、普段の開発でも気をつけたいポイントを一緒に見ていこうね
- 🦜 きなこ：あー、それは今日の話を聞いたあとだと、けっこう危ない橋だったかもね
![Caption: checkmark "One legitimate account per organization"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/099.png)
- 🦜 きなこ：規模の問題はあるけど、複数アカウントでレート制限を回避する行為自体が、今回の事案でも最大の摘発根拠になってるの
![Caption: checkmark "Do not bypass geo-restrictions with VPN/proxy"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/101.png)
- 🦜 きなこ：あと、地理的な制限をVPNやプロキシで回避するのもダメ。IPの相関は、今回みたいにちゃんと見られてるから
![Caption: checkmark "Do not use outputs to train competing models / avoid mass repetitive queries"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/103.png)
- 🦜 きなこ：出力を競合モデルの訓練に使うのも利用規約違反。同じような質問を大量に繰り返すのも、パターンとして検知の対象になるの
- 🦜 きなこ：そう。利用規約は破っても罰則がゼロってわけじゃない。契約違反や詐欺の構成で、ちゃんと責任を問われる可能性が残ってるんだよ

## まとめ

- 🐹 もっちー：いやー今日は勉強になったよ。ぼく完全に『提訴』だと思ってたもん
![今日のまとめ（3つのポイント）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/122.png)
- 🦜 きなこ：そこ、今日いちばん大事なとこだね。じゃあ3つのポイントで整理するね
![Diagram (1): not a "lawsuit" but a letter to the Senate](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V232/123.png)
- 🐹 もっちー：よし、まず1つめ。あれは裁判じゃなくて上院への書簡だったってことだよね？
- 🦜 きなこ：そう。ちゃんと提訴したわけじゃなくて、議会と当局に報告した形なの

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*