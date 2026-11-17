---
title: AIがPRを大量に作る時代、承認は誰がやる？Copilot承認の確認3点【解説記事】
emoji: 🤖
type: tech
topics:
- voicevox
- ai
- githubcopilot
- copilotcodereview
- github
published: true
---

# AIがPRを大量に作る時代、承認は誰がやる？Copilot承認の確認3点

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [AIがPRを大量に作る時代、承認は誰がやる？Copilot承認の確認3点](https://www.youtube.com/watch?v=RG47YekNGGU)
:::
@[youtube](RG47YekNGGU)

## この記事で分かること

- 🐹 もっちー：ねえきなこ、プルリクエストの承認って、人がするものだよね？
- 🐹 もっちー：えっ、AIが承認しちゃうの！？ じゃあ人は何するの？

## GitHubはPRを残してAIの承認を数える

- 🦜 きなこ：そう感じるよね。でも安心して。9月1日にプレビューで始まったときから、既定ではオフのままなんだよ
![承認のレベル別設定図: enterprise → organization → repository の3段で、Copilotの承認をオンにするかを選ぶ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/014.png)
- 🦜 きなこ：管理者がオンにする場所は3段あるの。enterprise、organization、repository、それぞれのレベルで選べるんだよ
![図: リポジトリ管理者が許可したファイルパスだけ、Copilotが承認できる](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/015.png)
- 🦜 きなこ：しかもリポジトリの管理者は、Copilotが承認していいファイルのパスまで、自分で絞り込めるの
- 🦜 きなこ：そう、そういう分け方ができる設定なの。ただし、このAIの承認が使えるのは、お金を払ってるプランだけなんだよ
![プランの対象一覧: Copilot Pro / Pro+ / Max / Business / Enterprise は対象、Free は対象外](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/018.png)
- 🦜 きなこ：対象はCopilotのPro、Pro+、Max、Business、Enterprise。Freeは入ってないんだよ
![対比カード: 承認の評価（approval assessment）だけ → 数えない ／ Copilotの承認 → 必須承認数に数える](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/020.png)
- 🦜 きなこ：ならないの。まとめコメントに付く承認の評価だけでは、必須承認の数には入らないって、公式にはっきり書いてあるよ

## Entireはdiffの代わりにスコアを見せる

![Entire の紹介カード：創業者 Thomas Dohmke（元GitHub CEO・現 Entire CEO）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/028.png)
- 🦜 きなこ：そう聞こえるよね。先に会社を紹介するね。作ったのは、元GitHub CEOのDohmkeさんなの
![資金調達カード：2026-02-10 発表／シード 6,000万ドル／評価額 3億ドル／リード Felicis](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/029.png)
- 🦜 きなこ：2026年2月10日に、評価額3億ドルで、6,000万ドルのシード資金を集めたって発表してるよ
![Entire CLI の説明図：AI が関わったコミットごとにチェックポイント（指示・会話・触ったファイル）を記録](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/031.png)
- 🦜 きなこ：最初はCheckpointsっていう名前の、Entire CLI。AIが関わったコミットごとに、指示や触ったファイルを記録するの
![提供状況カード：公開・プレビュー／ホストできるのは非公開リポジトリのみ（公開リポジトリは今後の機能）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/032.png)
- 🦜 きなこ：今はコードを置く場所そのものも、公開・プレビューで出してる。置けるのは、非公開リポジトリだけだよ
![料金カード：プレビュー中はエージェント利用分のみ従量課金／Code Hosting・Trails などは無料](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/033.png)
- 🦜 きなこ：料金ページだと、プレビュー中に払うのはエージェントの利用分だけ。置き場所やTrailsは無料なの
![Trails のスコア表示イメージ：push ごとに再計算される評価スコアの一覧（diff の代わりに表示）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/035.png)
- 🦜 きなこ：Trailsは、pushのたびに評価スコアを計算し直して、diffの代わりに一覧で見せるの

## Anthropicはマージ量そのものが増えた

![Anthropic公式Engineering Blog「Redesigning source control at Anthropic」（2026-10-13公開）のタイトルカード](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/043.png)
- 🦜 きなこ：じゃあAnthropicはどうなのか。10月13日の公式ブログで、まず大きな数字を出してきたの
![棒グラフ: Anthropicのモノレポの1日あたりマージ数（2026年5月 約2,500件 → 9月 30,000件超）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/045.png)
- 🦜 きなこ：1日にマージした数。5月は平均で約2,500件、それが9月には1日30,000件を超えたんだって
![グラフに「自社計測・第三者未検証」のラベルと、本文の表現「10x」の注記を重ねて表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/047.png)
- 🦜 きなこ：そう見えるよね。でも「全部AI」とは言ってなくて、コードの量が増えた話なの。本文は「10倍」で、自分で数えた数字だよ
![「今回は確認できていないこと」の一覧: 社内の新しいソース管理の仕組みの中身／「一般提供しない」の原文](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/049.png)
- 🦜 きなこ：そうなの。理由はClaudeがコードを書くからって本人たちの説明。社内の仕組みの中身は、今回確認できていないの
![カード: 「三者三様でも、自分のリポジトリで効くのはGitHubの設定」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/051.png)
- 🦜 きなこ：GitHubに置いてるなら、どれを選んでも結局効くのはGitHubの設定なんだよ。だから次は、そこを3つ見ていくね
- 🐹 もっちー：大きな数字？ ぼく、大きい数字は大好き！ 何の数なの？

## 自分のリポジトリで確認する3点

![①のカード：リポジトリ／Organizationの設定で「Copilotの承認 オン／オフ」と「承認できるファイルパス」を確認](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/053.png)
- 🦜 きなこ：3点だけだよ。1つめは、Copilotの承認がオンかオフか。それと、承認できるファイルパスね
![カード：既定はオフ／対象はCopilot Pro・Pro+・Max・Business・Enterprise／Freeは対象外](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/055.png)
- 🦜 きなこ：オンだと、Copilotの承認が人の承認と同じく必須承認数に数えられるの。既定はオフで、有料プランだけ。Freeは対象外だよ
![②の図：分岐保護／rulesetの設定画面で「必須承認数」と「Dismiss stale approvals」の位置を示す](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/057.png)
- 🦜 きなこ：分岐保護かrulesetで、必須承認数とDismiss stale approvalsを見て。新しいpushで、Copilotの承認は取り消されるからね
![図：中身が変わらないスタックをRebase stackで更新→Dismiss stale approvalsが有効でも承認が残る](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/059.png)
- 🦜 きなこ：例外があるの。中身が変わらないスタックをRebase stackで更新すると、取り消す設定でも承認が残るんだよ
![カード：Stacked pull requests 2026年10月6日 GA](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/061.png)
- 🦜 きなこ：そう。Stacked PRは10月6日にGAになったばかりだから、使うならこの例外は覚えておいてね
![③の図：auto-merge＋Agent Merge（Watch and fix）→必須レビューとステータスチェックを満たすまで待機→マージ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/063.png)
- 🦜 きなこ：しないよ。Agent Mergeは失敗したワークフローやコンフリクトを直す係。auto-mergeと組んでも、必須レビューとステータスチェックを満たすまで待つの

## まとめ

![3点チェックリスト:「1. Copilot承認のオン／オフと承認できるパス」「2. 必須承認数と古い承認の取り消し」「3. 自動マージは必須要件を待つ」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/066.png)
- 🦜 きなこ：まとめるね。見るのは3つだけ。1つ目は、Copilotの承認がオンかどうかと、承認できるファイルパス
- 🦜 きなこ：2つ目は、必須承認数と、古い承認を取り消す設定。3つ目は、自動マージが要件を待つことだよ
- 🐹 もっちー：それって、どこで見ればいいの？
![リポジトリ設定のブランチ保護／ルールセット画面のイメージ。「必須承認数」「古い承認を取り消す」の項目を強調](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V315/069.png)
- 🦜 きなこ：リポジトリの設定にある、ブランチ保護かルールセットの画面を開いて。必須承認数と、古い承認の取り消しのオン・オフをメモするだけ

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*