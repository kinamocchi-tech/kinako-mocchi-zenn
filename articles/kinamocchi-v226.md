---
title: MCPにボタンが出せる時代へ｜MCP Apps・進捗表示・承認フローを徹底解説【解説記事】
emoji: 🤖
type: tech
topics:
- mcp
- ai
- elicitation
- streaming
- llm
published: true
---

# MCPにボタンが出せる時代へ｜MCP Apps・進捗表示・承認フローを徹底解説

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [MCPにボタンが出せる時代へ｜MCP Apps・進捗表示・承認フローを徹底解説](https://www.youtube.com/watch?v=_KJCJJaZN1k)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、AIって結局さ、返事はぜんぶ文章で返ってくるものでしょ？
- 🐹 もっちー：え、ボタン？　AIの返事の中に、ほんとに押せるボタンが出るってこと？
- 🐹 もっちー：それってもう、返事っていうより小さいアプリじゃない？
- 🐹 もっちー：それめっちゃ便利やん！　もう文章読んで自分で操作せんでええってことやろ？

## MCPはもう実験じゃない（18か月で何が起きたか）

![Line chart: 2 million (Nov 2024) rising to 97 million (Mar 2026) monthly SDK downloads](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/017.png)
- 🦜 きなこ：その印象、2024年で止まってるかも。SDKの月間ダウンロードが、2024年11月の約200万回から、2026年3月時点で9,700万回まで伸びてるの
![Governance handover card: Anthropic to Linux Foundation / AAIF, Dec 2025](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/019.png)
- 🦜 きなこ：しかも2025年12月に、MCPはLinux Foundation傘下のAAIFという団体に寄贈されたの。特定の一社のものじゃなくなった
![Flow: proposal, working group review, spec update](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/021.png)
- 🦜 きなこ：仕様が「思いつきで変わらない」ようになったの。提案して議論して決める手続きができて、企業も安心して乗れるようになった
![Audit log entries and an SSO login screen shown side by side](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/023.png)
- 🦜 きなこ：変わったのはそこだけじゃないの。監査ログの形をそろえたり、会社のログイン基盤とつなぐ認証を標準にしたり
![Shift diagram: hobby setup on the left, enterprise setup on the right](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/025.png)
- 🦜 きなこ：まさにそこ。個人が趣味で動かす前提から、会社が業務で動かす前提へ、要求水準ごと引き上げられたの
![Audit trail table with user, time, and action columns](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/027.png)
- 🦜 きなこ：誰がいつ何を実行したかを後から追える記録と、社員のアカウントでそのままログインできる認証。この二つは特に強く求められるの

## ①インタラクティブコンポーネント（返り値を3つに割る理由）

![A huge plain-text table filling the model context window](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/034.png)
- 🦜 きなこ：その反応わかる。じゃあ想像してみて。顧客データを100件取ってきて、それを全部テキストの表に直してAIに読ませたとするね
![Cost meter rising as the text table grows](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/036.png)
- 🦜 きなこ：そう。しかも表示するだけのデータなのに、AIの読む枠を丸ごと食い潰す。返事も遅くなる。ここがずっと無駄だったの
![Python tool function returning a dict with three labeled keys](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/037.png)
- 🦜 きなこ：サーバー側のコードで言うと、返り値の辞書に三つの欄を用意して、それぞれ別の相手に向けて詰めるイメージなの
![Response object split into three labeled fields](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/040.png)
- 🦜 きなこ：だから戻り値を三つに割るの。この分け方、名前がついてて、コンテントとストラクチャードコンテント、それとアンダースコアメタ
![Field 1 highlighted: short summary text for the LLM](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/043.png)
- 🦜 きなこ：コンテントはAIが読む一言。ダッシュボードを出したよ、くらいの短い文で十分なの
![Field 2 highlighted: typed data flowing to a chart, hidden from the LLM](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/044.png)
- 🦜 きなこ：ストラクチャードコンテントはUIが読む生データ。グラフを描くための数字が入ってて、AIからは見えないの

## ②Streaming と MRTR（切れても最初からにならない）

- 🦜 きなこ：その質問は大事だから、あとでちゃんと答えるね。先に白状すると、わたしが一番困ってたのは実は別のところなの
![Spinner frozen on screen with no progress information](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/055.png)
- 🦜 きなこ：重い処理を頼むと、終わるまで画面が沈黙するの。動いてるのか死んでるのか、こっちからは区別がつかない
- 🦜 きなこ：実務でつらいのは、通信そのものに時間制限があること。よくある構成だと数十秒で切られるし、関数を動かす基盤にも実行時間の上限があるの
- 🦜 きなこ：頼めても、途中で切れたら結果が受け取れなかったの。だから長い処理は最初から諦められがちだった
![Restaurant pager buzzing while the customer waits at a table](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/060.png)
- 🦜 きなこ：だから途中経過を流せるようになったの。混んでるレストランの呼び出しベル、あるでしょ。あれと同じ考え方
- 🦜 きなこ：そうなの。しかも途中で明らかに違う方向へ進んでたら、早めに止められる。これも進捗が見える効用なんだよ

## ③Elicitation（AIが人間にハンコをもらいに来る）

![Secretary at a bank counter holding a transfer slip](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/071.png)
- 🦜 きなこ：その怖さ、まさに三つ目の話なの。秘書に振り込みを頼む場面を思い浮かべてみて
![Bank pauses the transaction and hands over a signature form](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/073.png)
- 🦜 きなこ：そう。銀行が「これは社長の署名が要ります」って手を止めて、用紙を渡す。秘書は署名をもらってから戻る
- 🦜 きなこ：止まらない仕組みのままだと、権限を持たせるのが怖くて、結局読み取り専用でしか使えなかったの
![Server returns an input-required status instead of a result](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/079.png)
- 🦜 きなこ：サーバーは「入力が要る」という返事を返すだけなの。画面を出すのはクライアント側の仕事
![Sequence diagram: pause, user input, resend with same request ID, resume](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/080.png)
- 🦜 きなこ：ユーザーがフォームに答えたら、クライアントが同じ注文番号に答えを添えて、もう一度投げ直す。それで処理が続きから走るの
- 🦜 きなこ：しかも、これがあると認証もきれいに書けるの。途中でログインしてもらって、その結果を持って続きを進められる

## 既存サーバーは壊れるのか（Graceful Degradation の作法）

- 🦜 きなこ：その心配、さっきの「どのアプリでもUIが出るの？」と同じ根っこなの。ここでまとめて答えるね
![Optional extension badge attached to the UI feature](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/090.png)
- 🦜 きなこ：描けないよ。だからUIの仕組みは、必須じゃなくて追加のオプションという位置づけになってるの
- 🦜 きなこ：実装をサボると本当に真っ白になるの。だから作る側に手順が決められてる。ここは守ってほしいところ
![Handshake step: client capability check during initialization](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/093.png)
- 🦜 きなこ：まず最初のつなぎ込みで、相手がUIに対応してるかを聞く。これが機能検知ね
![Two client types calling the same server: GUI app and terminal](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/094.png)
- 🦜 きなこ：実際、対応しているアプリと、文字だけのターミナルから使う人が、同じサーバーを同時に叩くことになるの
![Two branches: UI-capable client renders a panel, CLI client receives text](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/096.png)
- 🦜 きなこ：対応してなければ、UI前提のツールは出さない。出すなら、文章だけで完結する返事を必ず用意しておく

## MCPとA2Aは競合しない（境界線の話）

![Cluttered protocol logos being sorted into two lanes](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/108.png)
- 🦜 きなこ：別にあるよ。でも喧嘩はしないの。担当してる区間が、そもそも違うから
![Boundary diagram: agent to tool layer labeled MCP](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/110.png)
- 🦜 きなこ：MCPはもともと、エージェントと道具のあいだをつなぐために作られたの。データベースやAPIに接続する側ね
![Boundary diagram: cross-organization agent to agent layer labeled A2A](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/111.png)
- 🦜 きなこ：A2Aが担当するのは、組織をまたいだエージェント同士のあいだ。よその会社のエージェントに仕事を頼む側
- 🦜 きなこ：分かれるの。境目は「相手が自分で判断するかどうか」。データベースは判断しないけど、エージェントは判断するから
![ACP shown as a dashed box merged into A2A, dated 2025-08](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/116.png)
- 🦜 きなこ：ACPのことだね。ただ、あれは2025年8月にA2Aへ統合されて、今は単体では動いていないの
- 🦜 きなこ：具体的にすると分かりやすいよ。社内の顧客データベースから情報を取ってくる、これは道具につなぐ話だからMCP

## まとめ

![Summary card with three icons: UI, progress, approval](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/126.png)
- 🐹 もっちー：今日の三つ、言い直してみるね。画面が出せる、途中経過が見える、危ないところで止まる
- 🦜 きなこ：完璧。しかも三つとも追加のオプションだから、今のサーバーを止めずに順番に足していけるの
![Three step roadmap card](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V226/128.png)
- 🦜 きなこ：順番も思い出しておくね。まず戻り値を分ける、次に画面を足す、最後に危ない操作へ承認を挟む
- 🐹 もっちー：後ろに行くほど、影響が大きい変更になるってことか

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*