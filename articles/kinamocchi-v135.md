---
title: GPT-5.4-Cyber対Mythos！OpenAI vs Anthropicのサイバー戦略【解説記事】
emoji: 🤖
type: tech
topics:
- ai
- tac
- cybergym
- bountybench
- voicevox
published: true
---

<!-- グラレコ:graphreco -->
![GPT-5.4-Cyber対Mythos！OpenAI vs Anthropicのサイバー戦略【解説記事】｜グラレコ要約](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/V135_graphreco.png)

# GPT-5.4-Cyber対Mythos！OpenAI vs Anthropicのサイバー戦略

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [GPT-5.4-Cyber対Mythos！OpenAI vs Anthropicのサイバー戦略](https://youtu.be/gWe1LNKuf2g)
:::

## この記事で分かること

- 🐹 もっちー：そうそれ！で、結局どっちが最強なの？やっぱ一番強いやつを作ったところが、そのまま勝ちなんでしょ？
- 🐹 もっちー：えっ、最強AI同士なのに差がないの！？じゃあいったい、何で勝ち負けが決まるっていうの？
- 🐹 もっちー：配り方？AIに配り方なんてあるの？みんな同じように売るだけじゃないんだ、知らなかった
- 🐹 もっちー：同じ週に正反対！？なんやそれ、めっちゃ気になるやん！はよ続き教えてや！

## そもそも何者？ — 能力差は1.3ポイントの誤差

![サイバーAIが脆弱性を発見するイメージ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/018_cyber_ai_vulnerability.png)
- 🦜 きなこ：ざっくり言うとね、ソフトの中に隠れたバグや弱点を、人間の専門家よりずっと速く見つけられる、頼れるAIなの
![Mythosの発見実績リスト](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/019_mythos_achievements.png)
- 🦜 きなこ：Anthropicのは「Mythos」。なんと27年も誰も気づかなかったOpenBSDの欠陥を見つけたの
![Firefox 2週間で22件のCVE](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/021_firefox_cve.png)
- 🦜 きなこ：そうなの。しかもFirefoxでは、たった2週間で22件もの脆弱性を見つけて、ちゃんと直したんだよ
![UK AISI 専門家級CTF 73%達成](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/023_uk_aisi_ctf.png)
- 🦜 きなこ：イギリスの評価機関の試験でも、専門家級の難しい問題を73%も解いたの。本当にすごい数字なんだよ
![Cybench ほぼ満点](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/024_cybench_score.png)
- 🦜 きなこ：昔からある定番テスト「Cybench」だと、Mythosはもうほぼ満点。テストのほうが追いつけてないの
- 🦜 きなこ：うまいこと言うね。Anthropic自身も「今のテストじゃ進歩を測れない」って認めてるくらいなの

## OpenAIの賭け — 身元確認して『広く・速く・商用に』

![OpenAI戦略「広く・速く・商用に」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/037_openai_strategy.png)
- 🦜 きなこ：まずOpenAIから。もともと2023年から地道に強化してきて、今のキーワードは「広く商用に」なの
![TAC 段階アクセス図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/038_tac_access_diagram.png)
- 🦜 きなこ：中心にあるのがTAC、トラステッド・アクセス・フォー・サイバーっていう仕組みなの
- 🦜 きなこ：まさにそう。基本のAPIから、身元確認した人、サイバー許可した人、と段階的に解禁していくの
![Aardvark/Codex Security 30日で120万コミット](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/042_aardvark_codex.png)
- 🦜 きなこ：出てるよ。OpenAIのバグ発見AIは、たった30日で120万件ものコードを調べ上げたの
![792件のCritical脆弱性を発見](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/044_critical_vulns.png)
- 🦜 きなこ：その中から、危険度の高い深刻なバグを792件も発見。本物のCVEとして正式に登録もされたの
- 🦜 きなこ：しかもOpenAIは自社の基準で能力を「High」、危険な最高ランクのすぐ一歩手前だって認めてるの

## Anthropicの賭け — 限定して『狭く・慎重に・公益で』

![Anthropic戦略「狭く・慎重に・公益で」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/060_anthropic_strategy.png)
- 🦜 きなこ：そう、まさに真逆。Anthropicのキーワードは「狭く、慎重に、公益のために」なの
![「一般提供しない」引用カード](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/061_no_public_release.png)
- 🦜 きなこ：しかもね……Anthropicは、あの最強のMythosを「一般には提供しない」って、はっきり言い切ったの
- 🦜 きなこ：ふふ、その気持ちはすごく分かるよ。でもね、ちゃんとした理由があるの
- 🦜 きなこ：強すぎる能力を誰でも使えるようにすると、守る人だけじゃなく、攻撃する側にも力を与えちゃうの
![BountyBench: 防御型 vs 攻撃型](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/066_bountybench.png)
- 🦜 きなこ：実はね、AIには「守りが得意なタイプ」と「攻めが得意なタイプ」があるって分かってきたの
- 🦜 きなこ：テストでもAnthropic系は「攻撃」のほうが得意って出てるの。だからこそ、配り方に慎重になるんだよ

## なぜ真逆になった？ — 攻撃のAI自律化という現実

- 🦜 きなこ：理由のひとつが、サイバー攻撃の世界そのものが、もう昔とは変わっちゃったことなの
- 🦜 きなこ：攻撃そのものを、人間じゃなくてAIが自分でやる時代になったの。これがいちばん大きいの
![AI自律攻撃 80〜90%（GTG-1002事件）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/083_ai_autonomous_attack.png)
- 🦜 きなこ：Anthropicが去年11月に見つけた攻撃では、なんと攻撃の8〜9割をAIが自分で実行してたの
- 🦜 きなこ：怖いよね。実際この攻撃でも、人間が手を出したのは数回だけ。あとは全部AI任せだったの
![攻撃のhandoff時間 22秒](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/086_attack_handoff_22sec.png)
- 🦜 きなこ：しかも攻撃から次の攻撃へ移るスピードも、わずか数十秒まで縮んでるって報告もあるの
- 🦜 きなこ：そう。だからこれは、もう一部の専門家だけの話じゃなくて、わたしたちみんなに関わる問題なんだよ

## 顧客の答え — 両方に賭ける／ルールが決め手に

- 🦜 きなこ：それがね……答えは「どっちも」なの。びっくりするけど、これが現実なんだよ
![両陣営にダブル参加する企業のベン図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/103_venn_diagram_both.png)
- 🦜 きなこ：CrowdStrikeやPalo Alto、JPモルガン、NVIDIA、Ciscoは、両方の枠組みに参加してるの
- 🦜 きなこ：ふふ、それが賢いんだよ。どっちのやり方が正解か、まだ誰にも分からないからなの
![CrowdStrike Charlotte AI AgentWorks（モデル中立）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/106_crowdstrike_agentworks.png)
- 🦜 きなこ：セキュリティ会社のCrowdStrikeなんて、複数のAIを並べて選べる仕組みまで作ったの
- 🦜 きなこ：そう。お客さん側は「どっちが最強か」より「どっちが信頼できるか」を、じっくり見極めてる段階なの
![各国のAI規制マップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/110_global_ai_regulation.png)
- 🦜 きなこ：大きいのが「ルール」なの。世界中で、AIを安全に使うための法律や指針が整い始めてるんだよ

## まとめ

![まとめ: OpenAI型『広く商用』vs Anthropic型『狭く公益』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/123_summary_comparison.png)
- 🐹 もっちー：今日はすごく勉強になった。最強AIの勝負って、能力の数字だけじゃ決まらないんだね
- 🦜 きなこ：そう。差別化はもう能力じゃなくて「誰に、どう配るか、どう信頼を積み上げるか」に移ったの
- 🐹 もっちー：OpenAIは広く商用で味方を増やす、Anthropicは狭く公益で先回りする。哲学が真逆ってことか
![3点まとめ: ①能力は横並び ②勝負は配り方 ③決め手は信頼とルール](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V135/127_three_point_summary.png)
- 🐹 もっちー：整理すると、ひとつ、能力はもう横並び。ふたつ、勝負は配り方。みっつ、決め手は信頼とルール、だね
- 🦜 きなこ：完璧なまとめだね。その3つを押さえておけば、これからのサイバーAIのニュースがぐっと読みやすくなるよ

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*