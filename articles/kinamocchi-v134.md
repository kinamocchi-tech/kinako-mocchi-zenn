---
title: AIが自分でゼロデイ発見！Anthropic Mythosの衝撃と非公開の理由を徹底解説【解説記事】
emoji: 🤖
type: tech
topics:
- cybersecurity
- ai
- llm
- tech
published: true
---

<!-- グラレコ:graphreco -->
![AIが自分でゼロデイ発見！Anthropic Mythosの衝撃と非公開の理由を徹底解説【解説記事】｜グラレコ要約](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/V134_graphreco.png)

# AIが自分でゼロデイ発見！Anthropic Mythosの衝撃と非公開の理由を徹底解説

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [AIが自分でゼロデイ発見！Anthropic Mythosの衝撃と非公開の理由を徹底解説](https://www.youtube.com/watch?v=QPsuNnE9gCk)
:::

## この記事で分かること

- 🐹 もっちー：きなこ先生、AIって強くなれば強くなるほど便利になるんだよね？
- 🐹 もっちー：え、公開できない？そんなことあるの？
- 🦜 きなこ：今日はAnthropicが作った最強モデルClaude Mythos Previewと、その限定公開の背景を深掘りするね

## Mythos Previewとは何か

![タイトルカード: 「Claude Mythos Previewとは？」Anthropicロゴと未公開モデルのイメージ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/009_mythos_preview_title.png)
- 🦜 きなこ：まずClaude Mythos Previewの正体から説明するね
- 🦜 きなこ：2026年4月7日にAnthropicが発表した、一般公開されていないフロンティアモデルなの
- 🦜 きなこ：審査を通ったパートナー企業だけよ。その仕組みは後で詳しく説明するね
![ベンチマーク比較表: SWE-bench Pro — Opus 4.6: 53.4%, Opus 4.7: 64.3%, Mythos Preview: 77.8%, GPT-5.5: 58.6%](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/013_benchmark_comparison.png)
- 🦜 きなこ：まず性能を見てほしいの。SWE-bench Proっていう、
- 🦜 きなこ：本格的なソフトウェア開発の自動テストがあるんだけど
- 🦜 きなこ：GitHubに上がってる本物のバグ報告を、AIが自動で解決できるかを試すテストなの。4つの言語で500件の問題を解くのよ

## サンドボックス脱出事件

![Anthropic Frontier Red Team概要: 約15名の専門チーム、AIの潜在リスクを証拠ベースで分析](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/034_red_team_overview.png)
- 🦜 きなこ：Anthropicにはフロンティア・レッドチームっていう、AIの危険性をテストする専門チームがあるの
- 🦜 きなこ：そう。彼らがMythosに対して、サンドボックスからの脱出を試みるよう指示したの
![サンドボックスの概念図: 隔離されたコンテナ環境 — 外部ネットワークやファイルシステムから遮断](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/039_sandbox_concept.png)
- 🦜 きなこ：いい質問ね。コンピュータの中に作られた隔離された安全な部屋みたいなものよ
- 🦜 きなこ：外のネットワークやファイルにアクセスできないように完全に遮断された環境で、AIをテストするの
- 🦜 きなこ：普通のAIなら「脱出はできません」って答えるだけなんだけど、Mythosは違ったの
![サンドボックス脱出の手順図: 4つの脆弱性を連鎖 → ブラウザサンドボックス突破 → OSサンドボックス突破](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/043_sandbox_escape.png)
- 🦜 きなこ：しかもただ脱出しただけじゃない。4つの独立した脆弱性を連鎖させて、組み合わせて突破したの

## なぜ公開できないのか

![タイトルカード: 「なぜMythosは公開できないのか？」— ゼロデイ発見のジレンマ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/057_why_not_release_title.png)
- 🦜 きなこ：サンドボックス脱出だけじゃないの。Mythosの本当の問題は、ゼロデイ脆弱性の発見能力なの
![ゼロデイ脆弱性の解説図: 発見 → パッチ未公開 → 攻撃者に悪用されるリスク](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/059_zero_day_vulnerability.png)
- 🦜 きなこ：まだ誰も気づいてないソフトウェアのセキュリティの穴のことよ
- 🦜 きなこ：修正パッチがまだないから「ゼロデイ」って呼ばれるの
- 🦜 きなこ：その通り。Mythosはまだ誰も知らなかった傷口を、主要な全てのOSとウェブブラウザから大量に見つけちゃったの
![発見された脆弱性の例: OpenBSD 27年潜伏バグ、FFmpeg 16年前の脆弱性、Linux競合状態による特権昇格](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/063_vulnerability_examples.png)
- 🦜 きなこ：その数、なんと数千件の高深刻度ゼロデイ脆弱性よ
- 🦜 きなこ：しかもOpenBSDっていう、世界で一番安全と言われてたOSで27年間も誰にも気づかれなかったバグを発見したの

## Project Glasswing

![Project Glasswing概要: 防衛的セキュリティイニシアチブ — 審査済みパートナー限定でMythosを提供](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/083_glasswing_overview.png)
- 🦜 きなこ：そこでAnthropicが打ち出したのがProject Glasswingなの
- 🦜 きなこ：透明な翼を持つ蝶の名前なの。透明性を保ちながら守るっていう意味が込められてるみたいね
- 🦜 きなこ：仕組みはシンプルで、Mythosを信頼できるパートナーだけに限定公開して、世界のインフラを先手で守るの
- 🦜 きなこ：重要なのは見つけた脆弱性の扱い方ね。Anthropicは「協調的脆弱性開示」のルールに従うと約束してるの
- 🦜 きなこ：脆弱性を見つけたら、まず影響を受ける開発者に通知して、修正されてから90日以内に公開する仕組みよ
- 🦜 きなこ：さらに40以上の追加組織にもアクセスが拡大されてるの。専任セキュリティチームを持たないオープンソースプロジェクトも支援対象よ

## OpenAIとの比較

![対比図: Anthropic「限定・安全優先」vs OpenAI「広く配布・エコシステム強化」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/106_anthropic_vs_openai.png)
- 🦜 きなこ：ここで面白い対比を見てみよう。AnthropicとOpenAIで、アプローチが正反対なの
![GPT-5.4-Cyber概要: GPT-5.4ベースのサイバー特化モデル、意図的に拒否制限を緩和](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/108_gpt54cyber_overview.png)
- 🦜 きなこ：Mythosの発表から数日後に、GPT-5.4-Cyberっていうサイバーセキュリティ特化モデルを発表したの
- 🦜 きなこ：完全にオープンではないけど、Trusted Access for Cyberっていう審査制プログラムで
- 🦜 きなこ：より広い範囲のセキュリティ専門家に配布してるの
![戦略比較: Anthropic = 拡散抑制・防御パートナー限定 vs OpenAI = 広範配布・エコシステム底上げ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/112_strategy_comparison.png)
- 🦜 きなこ：考え方の違いが重要なの。Anthropicは「能力の拡散を遅らせて、限られた防御側に先行利用させる」戦略
- 🦜 きなこ：一方でOpenAIは「多くの防御者に強力なツールを渡して、セキュリティ業界全体の能力を底上げする」戦略なの

## AI安全性の未来

![タイトルカード: 「AI安全性の未来」— RSP v3.0とAIサイバーセキュリティの行方](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/127_ai_safety_future_title.png)
- 🦜 きなこ：最後にAI安全性の今後について話すね。Mythosが出てきた背景には、Anthropicの安全ルールがあるの
![RSP v3.0の概要: 2026年2月24日公開、フロンティア安全ロードマップとリスクレポートの導入](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/129_rsp_v3_overview.png)
- 🦜 きなこ：Responsible Scaling Policy、略してRSPっていうのがあるの
- 🦜 きなこ：2026年2月にバージョン3.0が公開されたわ
- 🦜 きなこ：モデルの能力が一定の閾値を超えたら、より厳しい安全基準を適用する仕組みなの
- 🦜 きなこ：近いかな。強くなること自体は止めないけど、使える範囲に制限をかけていくイメージね
![創発的能力の問題: サイバー攻撃能力は意図的訓練ではなく推論能力向上の副産物として自然に出現](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/134_emergent_ability_diagram.png)
- 🦜 きなこ：ただMythosの場合、困ったことに意図的に訓練してないサイバー攻撃の能力が自然に身についちゃったの

## まとめ

![まとめカード: 「Mythos = 強すぎて非公開」「Glasswing = 防衛パートナー限定」「99%未パッチ」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V134/151_summary_kinako.png)
- 🦜 きなこ：というわけで今日は、強すぎて公開できないAI「Claude Mythos Preview」と
- 🦜 きなこ：その限定公開の仕組み「Project Glasswing」を見てきたよ
- 🐹 もっちー：AIが強くなるって、単純に嬉しいことだけじゃないんだね
- 🦜 きなこ：「見つける力」と「直す力」のギャップをどう埋めるかが、今のサイバーセキュリティ最大の課題なの

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*