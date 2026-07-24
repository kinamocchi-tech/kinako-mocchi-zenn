---
title: Claude Code Channelsとは？Telegram・Discord・iMessage連携【解説記事】
emoji: 🤖
type: tech
topics:
- voicevox
- ai
- channels
- telegram
- discord
published: true
---

# Claude Code Channelsとは？Telegram・Discord・iMessage連携

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [Claude Code Channelsとは？Telegram・Discord・iMessage連携](https://www.youtube.com/watch?v=oB7y5t0_4Kw)
:::

## この記事で分かること

- 🐹 もっちー：飼い主がさ、パソコンの前にずっと座ってAIに指示出してるじゃん？
- 🐹 もっちー：あれ、スマホからできたらめっちゃ便利じゃない？
- 🐹 もっちー：えぇ！めっちゃすごいやん！スマホでAIにコード書かせられるん！？
- 🐹 もっちー：へぇ、でもスマホから指示して大丈夫なの？セキュリティ的に心配なんだけど

## Channels機能の概要と3つのプラットフォーム

- 🦜 きなこ：まずClaude Code Channelsがどういう機能か説明するね
![Claude Code Channelsの概念図（スマホ→チャットアプリ→Claude Code）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/018_channels_concept.png)
- 🦜 きなこ：ひとことで言うと、チャットアプリからClaude Codeに指示を送れる機能だよ
![3つのプラットフォームロゴ一覧（Telegram/Discord/iMessage）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/020_platform_logos.png)
- 🦜 きなこ：近いけど、対応してるのはTelegram、Discord、iMessageの3つだね
- 🦜 きなこ：まだリサーチプレビュー段階だから、今後増える可能性はあるよ
![Claude Code Channels ロゴ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/022a_channels_logo.png)
- 🦜 きなこ：名前の「Channels」は、複数のチャットチャンネルをAIとつなぐという意味から来てるんだよ
![リリース情報（v2.1.80、2026年3月20日、リサーチプレビュー）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/023_release_info.png)
- 🦜 きなこ：2026年3月20日に、バージョン2.1.80で公開されたばかりなの

## MCPアーキテクチャの仕組み

- 🦜 きなこ：ここからは、Channelsの中身の仕組みを見ていくよ
![MCPアーキテクチャ概念図（Claude Code ← MCP → Channels Plugin → チャットアプリ）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/040_mcp_architecture.png)
- 🦜 きなこ：ChannelsはMCPサーバーとして動作するプラグインなの
![MCPの図解（AI ⇔ 共通プロトコル ⇔ 外部ツール群）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/042_mcp_protocol.png)
- 🦜 きなこ：Model Context Protocol、AIと外部ツールをつなぐ共通ルールだよ
- 🦜 きなこ：いいたとえだね。MCPがあるおかげで、TelegramでもDiscordでも同じように使えるの
![Bunランタイム上のMCPサーバー構成図（Bun → MCPサブプロセス → 各プラットフォームAPI）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/045_bun_runtime.png)
- 🦜 きなこ：技術的にはBunっていうランタイムの上で、サブプロセスとして動いてるの
- 🦜 きなこ：メインのClaude Codeの処理の中で、別の小さな処理として独立して動くってことだよ

## 3層セキュリティモデル

- 🦜 きなこ：じゃあ次は、Channelsのセキュリティモデルを解説するよ
![3層セキュリティ概要図（第1層: ログイン、第2層: ペアリング、第3層: 許可リスト）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/062_security_overview.png)
- 🦜 きなこ：実は3層構造になってるの。かなりしっかりしてるよ
![第1層: claude.aiログイン認証（Pro/Max必須、Console/APIキーは不可）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/064_login_auth.png)
- 🦜 きなこ：第1層は、claude.aiのログインが必須ってこと。ProかMaxのサブスクリプションが要るの
![第2層: ペアリングコード認証の流れ（初回接続 → DM受信 → コード入力 → 認証完了）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/066_pairing_code.png)
- 🦜 きなこ：第2層は、ペアリングコード認証だよ。初めて接続するとき、DMでコードが送られてくるの
![第3層: Sender Allowlist（許可ユーザーIDリスト、未許可はサイレントに破棄）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/068_sender_allowlist.png)
- 🦜 きなこ：そうそう。そして第3層がSender Allowlist。許可したユーザーのIDだけを受け付けるの
- 🦜 きなこ：コードを実行できるツールだからこそ、厳しくないとダメなの

## 開発者たちの実践記録——スマホからのコード指示

![「開発者の実践記録」テロップ表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/090_developer_stories.png)
- 🦜 きなこ：じゃあ次は、Channelsを実際に使ってる開発者の事例を見てみよう
![MacStories John Voorhees氏の事例テロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/092_john_voorhees.png)
- 🦜 きなこ：まずはMacStoriesのジョン・ヴォーヒーズさん
![iPhone → Telegram → Claude Code → Xcode Build の流れ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/093_dev_workflow.png)
- 🦜 きなこ：この人、iPhoneからTelegram経由でiOSアプリのビルドとデプロイに成功してるの
![Ewan Mak氏 スマホからサイト移行監視のイメージ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/095_site_migration.png)
- 🦜 きなこ：次はテンテンのイワン・マクさん。40分間のクライアントサイト移行を、スマホから監視したの
![Aleksandar Mirilovic氏のエピソード紹介テロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/097_aleksandar.png)
- 🦜 きなこ：そしてアレクサンダー・ミリロヴィッチさんのエピソードが面白くて
- 🦜 きなこ：ドイツ語の試験に遅刻しちゃって、Telegramで音声メッセージを送ったの

## OpenClawとの対立——OSSの野心とAnthropicの反撃

![「OpenClaw vs Claude Code Channels」テロップ表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/111_openclaw_vs.png)
- 🦜 きなこ：さて、ここでChannelsの話と切っても切れない存在を紹介するね。OpenClawっていうOSSプロジェクト
![名前の変遷: Clawdbot → Moltbot → OpenClaw](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/113_name_history.png)
- 🦜 きなこ：オーストリアのピーター・シュタインバーガーさんが作ったツールで、最初はクロウドボットって名前だったの
- 🦜 きなこ：でもアンソロピックから商標で怒られて、モルトボット、そしてオープンクロウって名前を変えていったの
![OpenClaw対応プラットフォーム6種のアイコン一覧](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/116_openclaw_platforms.png)
- 🦜 きなこ：WhatsApp・Telegram・Discord等、6つのプラットフォームに対応してて、Channelsより広いの
![GitHub Stars: 247,000+ のテロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/117_github_stars.png)
- 🦜 きなこ：GitHubスターも2026年3月時点で25万を超えていて、すごい人気だったの
![「2026年2月: Steinberger氏 → OpenAI入社」テロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/119_steinberger_openai.png)
- 🦜 きなこ：ところがね、2026年2月にシュタインバーガーさんがOpenAIに入社したの

## 2026年3月——Claude Code史上最大のアップデート月

![「2026年3月 Claude Code大進化」テロップ + タイムライン](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/131_march_evolution.png)
- 🦜 きなこ：実はね、Channelsだけじゃないの。2026年3月はClaude Code史上最大のアップデート月だったんだよ
![Voice Mode: /voice コマンド → プッシュ・トゥ・トーク](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/133_voice_mode.png)
- 🦜 きなこ：まず3月3日にボイスモードが追加されたの。スラッシュvoiceで起動できるんだよ
![20言語対応 / 転写レイテンシ 1〜2秒](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/134_20_languages.png)
- 🦜 きなこ：プッシュ・トゥ・トークで20言語に対応。転写レイテンシは1から2秒だよ
![Auto Mode（3月24日）テロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/136_auto_mode.png)
- 🦜 きなこ：次に3月24日にオートモードがリリースされたの
![2層安全システム: インジェクション検出 + 分類器 / 偽陽性率0.4%](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/137_safety_system.png)
- 🦜 きなこ：2層の安全システムで、プロンプトインジェクション検出と分類器が動いてるの。偽陽性率は0.4パーセント
![Dispatch + Computer Use（3月23日）テロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/139_dispatch_computer_use.png)
- 🦜 きなこ：かなり精度が高いよね。そして3月23日にはディスパッチとコンピューターユースも来たの

## まとめ

![「まとめ」テロップ表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/147_summary.png)
- 🐹 もっちー：いやー、今日はChannelsの話、めっちゃ面白かったなぁ
- 🐹 もっちー：TelegramとかDiscordとかiMessageから、コードの指示ができるってだけでもすごいのに
- 🐹 もっちー：実際にスマホからアプリのビルドまでできちゃうし、寝てる間にバグ調査もしてくれるんだよね
- 🐹 もっちー：しかもOpenClawとの競争もあって、どんどん進化してるし
![「スマホとターミナルの境界が消える」テロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V084/151_mobile_terminal.png)
- 🦜 きなこ：もっちーの言う通りだね。今回のポイントは、スマホとターミナルの境界がなくなっていくってことだと思うの

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*