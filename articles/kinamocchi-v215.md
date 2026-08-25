---
title: Windsurfが消えた日｜Devin Desktop改名で入れ替わったもの【解説記事】
emoji: 🤖
type: tech
topics:
- windsurf
- cognition
- cursor
- ai
- llm
published: true
---

# Windsurfが消えた日｜Devin Desktop改名で入れ替わったもの

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [Windsurfが消えた日｜Devin Desktop改名で入れ替わったもの](https://www.youtube.com/watch?v=u1BCWc9to9o)
:::

## この記事で分かること

- 🐹 もっちー：なあきなこ、朝パソコン開いたら、使ってたエディタの名前が勝手に変わってたら、どう思う？
- 🦜 きなこ：そんなことある？って思うよね。でも2026年6月2日、AIコーディングエディタのWindsurfで、それが本当に起きたの
- 🐹 もっちー：え、勝手に！？　僕の設定とか拡張機能は、消えてないの？
- 🐹 もっちー：入れ替わる！？　それ、削除されるのと何が違うの？

## 何が起きたのか — 2026年6月2日の事実

![Timeline card: 2026-06-02, Windsurf IDE renamed to Devin Desktop, delivered as an automatic over-the-air update](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/014.png)
- 🦜 きなこ：そこが面白いところ。今回は、いつものアップデートと同じ形で、自動で配信されたの。ユーザーは何もしてないのに切り替わった
![Checklist card: editor, extensions, keybindings, LSP settings, workflows all preserved after rebrand](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/016.png)
- 🦜 きなこ：残ったものから言うね。エディタそのもの、拡張機能、キーバインド、それから言語サーバーの設定。全部そのまま
- 🦜 きなこ：ふふ、そこ大事だよね。そもそもこの手のエディタは、VS Codeの拡張機能や設定をそのまま扱える土台の上に建ってるの
- 🦜 きなこ：プランも価格も、そのまま据え置きで移ったの。で、ここからが本題。会社がこの製品をどう説明したかが独特なんだよ
![Layer diagram: full IDE as the outer shell, agent manager embedded inside (not the reverse)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/022.png)
- 🦜 きなこ：違うの。エージェントマネージャーを内蔵したフルIDE、その逆ではない、って言い方をしてる
- 🦜 きなこ：たぶん、線を引きたかったんだと思う。AIが主役でエディタがおまけ、じゃなくて、あくまでエディタが主役。その中にAIの管理画面が入ってる、って順番

## 数日で決着した争奪戦 — 経営陣だけ抜かれた会社に何が残ったか

![Split-company diagram: leadership and assets going to different buyers](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/037.png)
- 🦜 きなこ：そう思うよね。私も最初はそのつもりで調べたの。でも実際に起きたのは、会社を切り分けて別々の相手に渡す形だった
![Timeline step 1 (July 2025): Google DeepMind hires Windsurf CEO Varun Mohan and co-founder Douglas Chen in a reverse acquihire deal](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/039.png)
- 🦜 きなこ：順番に見ていくね。まず2025年7月、GoogleのDeepMindが、Windsurfの最高経営責任者と共同創業者、それに研究のリーダーを引き抜いたの
![Number card: about $2.4B - Google's license-and-hire deal for Windsurf leadership](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/041.png)
- 🦜 きなこ：報じられている規模で、およそ24億ドル。技術のライセンスと人の雇用をセットにした取り引きなの
- 🦜 きなこ：アリなの。しかもこの数日前まで、別の相手が会社ごと買う話を進めてたんだよ
![Timeline step 2: OpenAI's reported ~$3B acquisition offer expires](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/045.png)
- 🦜 きなこ：OpenAI。買収の申し出をしていたけど、その提案は期限切れで流れたの。金額はおよそ30億ドルと報じられてる
![Company card: Cognition, maker of the autonomous coding agent Devin, CEO Scott Wu](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/047.png)
- 🦜 きなこ：そこで出てくるのがCognition。自律型のコーディングエージェント、Devinを作ってる会社なの

## 名前が変わり続けた会社 — よくある勘違いを正す

![Correction card: company rename Codeium to Windsurf happened 2025-04-04, not April 2024](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/067.png)
- 🦜 きなこ：そこ、みんなが間違えるところ。会社の名前がCodeiumからWindsurfに変わったのは、2025年の4月4日なの
![Timeline card: Nov 2024 Windsurf Editor launch / Apr 2025 company rename - two different events](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/069.png)
- 🦜 きなこ：無理もないの。2024年11月に、Windsurfっていう名前のエディタ自体は先に出てるから
![Order diagram: product launch first, company rename second](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/071.png)
- 🦜 きなこ：そういう順番。だから2025年4月の出来事は、新しいエディタが誕生した日じゃなくて、会社の看板をそろえた日なの
![Pattern card: company names keep chasing product names](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/073.png)
- 🦜 きなこ：この、会社の名前と製品の名前がずれる現象。実は今回の改名も、まったく同じ形をしてるの
![History strip: plugin era, standalone editor era, agent era](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/075.png)
- 🦜 きなこ：開発ツールの世界ではね、プラグインから独立エディタ、そしてエージェントへと主役が移るたびに、社名が製品名を追いかけてきたの
- 🦜 きなこ：そう。しかもこの四つの出来事、間隔がどんどん短くなってるの

## 『何も削除されない』の裏側 — 入れ替わったのは心臓部

![Component card: Cascade, the agent built into Windsurf that reads, edits and runs code](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/092.png)
- 🦜 きなこ：Windsurfには、Cascadeっていう内蔵のAIエージェントがいたの。コードを読んで、直して、動かしてくれる相棒
![Replacement diagram: Cascade agent scheduled for end-of-life on 2026-07-01, replaced by a Rust-rewritten agent named Devin Local](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/094.png)
- 🦜 きなこ：2026年7月1日でサポート終了の予定とされていて、Devin Localっていう別のエージェントに置き換わる見込みだったの
- 🦜 きなこ：ちなみにDevin Localは、動作が速くて壊れにくいRustっていう言語で書き直されてるの
![Two-layer diagram: editor layer preserved / agent layer replaced](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/098.png)
- 🦜 きなこ：そう。ただね、公式がウソをついたわけでもないの。見てる層が違うだけ。設定も拡張機能もキーバインドも、そこは本当にそのまま
- 🦜 きなこ：でもエディタって昔から、見える層と、裏で実際に動くエンジンを分けて作られてきたの。会社が変わると、まず入れ替わるのは裏側なんだよ
- 🦜 きなこ：そのたとえ、すごくいいと思う。住んでる感じは同じ。でも替わったのは、その家の心臓にあたるところなの

## 三つ巴の現在地 — 差がつくのはコード生成能力ではない

![Comparison card: Cursor, Devin Desktop and Google Antigravity are all VS Code forks with LLMs on top](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/122.png)
- 🦜 きなこ：Cursor、今回のDevin Desktop、それにGoogleのAntigravity。2026年1月の時点で、三つとも同じVS Codeを土台にしてるの
- 🦜 きなこ：そこには理由があると思ってるの。開発ツールって、みんなが積み上げてきた拡張機能と、指が覚えたキー操作を捨てられないんだよ
![Background note: forks reuse the existing extension ecosystem and muscle memory instead of asking users to switch](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/125.png)
- 🦜 きなこ：どんなに賢い新しいエディタが出ても、乗り換えの壁はそこだった。だから今の世代は最初から同じ土台に乗ってる、と私は見てるの
- 🦜 きなこ：その通り。しかも、その上の差は、どっちが賢いコードを書くかじゃないの
![Differentiation axis card: autonomy level, workflow design, and how much control the developer keeps](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/129.png)
- 🦜 きなこ：どこまでAIに任せるか、どういう手順で進めるか、そして人がどれだけ手綱を握れるか。差はそこに移ってるの
![Profile card 1: Cursor emphasizes speed and visual polish](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/131.png)
- 🦜 きなこ：まずCursorは、速さと画面の洗練を重視してる。とにかく気持ちよく手が動くほうへ倒してるの

## まとめ

![Summary card - confirmed: 2026-06-02 rebrand, settings and pricing carried over, acquisition on 2025-07-14](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/151.png)
- 🦜 きなこ：今日の確定してることを、もう一度まとめるね。2026年6月2日にWindsurfがDevin Desktopになって、設定も価格もそのまま引き継がれた
- 🦜 きなこ：その前に、2025年7月14日の買収があって、経営陣はGoogleへ移ってた。ここまでは公式と大手報道で確認できてる
![Summary card - unverified: official deal terms, head-to-head benchmarks, 2026 pricing tiers](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V215/153.png)
- 🦜 きなこ：逆に確認できてないのは、買収額の正式な条件、三製品のベンチマーク、それに2026年の細かい料金。ここは断定しないでおくね
- 🐹 もっちー：この年表、あとで絶対また見たなるやつや。保存しとこ！

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*