---
title: 'MCP 2026: 業界標準から『セキュリティ悪夢』へ ― 月間9700万DLの光と影【解説記事】'
emoji: 🤖
type: tech
topics:
- mcp
- modelcontextprotocol
- claude
- ai
- linuxfoundation
published: true
---

# MCP 2026: 業界標準から『セキュリティ悪夢』へ ― 月間9700万DLの光と影

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [MCP 2026: 業界標準から『セキュリティ悪夢』へ ― 月間9700万DLの光と影](https://www.youtube.com/watch?v=HMvgiR2snQ8)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、MCPって知ってる？AIの世界のUSB-Cみたいなもんでしょ？
- 🐹 もっちー：業界標準になってOpenAIもGoogleも使ってるのに、何が問題なの？そんなん聞いてないで！
- 🐹 もっちー：え、悪夢って何？便利なだけじゃないの？
- 🦜 きなこ：標準化は便利だけど、攻撃者にとっても入口が一つになるってことなの。今日はその光と影を深掘りしていくね

## MCPの基本と爆発的普及

![MCPの基本構造図: AIアプリ（クライアント）とツール・データソース（サーバー）がJSON-RPC 2.0で通信する概念図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/009_MCPの基本構造図.png)
- 🦜 きなこ：まずMCPの基本から整理するね。MCPはModel Context Protocolの略で、AIと外部ツールを繋ぐためのオープンな規格なの
- 🦜 きなこ：GitHubとかSlack、データベース、Google Driveとか色々だよ。AIが直接これらのサービスを操作できるようになるの
![N×M問題の図解: 左にAIモデル群（Claude、ChatGPT、Gemini）、右にツール群（GitHub、Slack、DB）、全てが個別に接続線で結ばれている複雑な図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/013_NxM問題の図解.png)
- 🦜 きなこ：前はAIモデルごとに個別の接続を作る必要があったの。例えばClaude用、ChatGPT用、Gemini用って全部別々
![N+M解決の図解: 中央にMCPロゴ、左のAIモデル群と右のツール群がMCPを介してシンプルに接続される図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/015_N+M解決の図解.png)
- 🦜 きなこ：そう、これをN×M問題って呼ぶんだけど、MCPはこれをN+Mに変えたの。USB-Cみたいに一つの規格で全部繋がる世界にした
- 🦜 きなこ：2024年11月にAnthropicが発表して、そこから一気に広まったの
![MCP採用タイムライン: 2024年11月Anthropic発表 → 2025年3月OpenAI → 2025年4月Google → 2025年5月Microsoft の時系列図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/018_MCP採用タイムライン1.png)
- 🦜 きなこ：OpenAIが2025年3月に対応を表明、GoogleもGeminiでサポート、MicrosoftもWindows 11でネイティブ対応を発表した

## 2026年に噴出したセキュリティ危機

![OX Security報告のヘッドライン画像: 「The Mother of All AI Supply Chains」というタイトルと2026年4月15日の日付](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/025_OX_Security報告のヘッドライン.png)
- 🦜 きなこ：まず一番衝撃的だったのが、2026年4月のOX Securityの発表。MCPの公式SDKに「設計上の欠陥」があると報告したの
![STDIO脆弱性の図解: MCPサーバーが標準入出力（STDIO）経由で接続 → 悪意あるコマンドが注入される流れを矢印で示す](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/027_STDIO脆弱性の図解.png)
- 🦜 きなこ：そう。MCPのSTDIOっていう通信方式のデフォルト設定が安全じゃなかったの。これを使うと、悪意のある相手がパソコン上で好きなコマンドを実行できてしまう
- 🦜 きなこ：しかもOX SecurityはAnthropicに報告したんだけど、Anthropicは「これは仕様通りだ」って修正を拒否したの
- 🦜 きなこ：その通り。しかも問題の根深いところは、これがSDKのバグじゃなくて、プロトコルの設計そのものに起因してること
- 🦜 きなこ：OX Securityが「仕様レベルの体系的欠陥」と公表したの
![セキュリティ研究者の警告: OX Security → Anthropicへの報告 → 修正拒否 → 業界騒然の流れ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/030d_セキュリティ研究者の警告フロー.png)
- 🦜 きなこ：そうなの。しかもAnthropicがこの報告に対して根本的な修正を拒否したことで、セキュリティ研究者たちの間で大きな議論になった

## なぜ標準化がリスクを生むのか

![標準化の逆説の概念図: 左「開発者にとって: 一つの規格で全部繋がる = 便利」→ 右「攻撃者にとって: 一つの攻撃手法で全部突破できる = 効率的」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/046_標準化の逆説の概念図.png)
- 🦜 きなこ：いい質問だね。さっきのUSB-Cの例えで考えてみて。全部の機器がUSB-Cで繋がるのは便利だけど、もしUSB-Cの規格自体に穴があったら？
- 🦜 きなこ：そう。MCPを攻略すれば、Claude、ChatGPT、Gemini、Cursor、全部まとめて攻撃できるの。攻撃者にとってはこれ以上ない効率のいいターゲットなんだよ
![学術研究の要点: 「MCP-38論文: 38の脅威カテゴリー」「MCPSecBench: 17の攻撃タイプ」「既存の保護機構の成功率は30%未満」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/049_学術研究の要点.png)
- 🦜 きなこ：学術論文でもこの問題が分析されていて、MCPの仕様から38の脅威カテゴリーが導出されているの
- 🦜 きなこ：特に根本的なのが、AIがツールを選ぶとき、そのツールの説明文だけを頼りに判断してる点なの
- 🦜 きなこ：論文ではこれをsemantic attack surfaceって呼んでる。意味レベルの攻撃面ってこと
![Shadow MCP概念図: 企業ネットワーク内に公式MCPサーバー（管理下）と非公式MCPサーバー（管理外）が混在する図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/052b_Shadow_MCP企業ネットワーク図.png)
- 🦜 きなこ：企業の中で勝手にMCPサーバーを立てちゃう現象のこと。クラウドの初期にあったShadow ITと同じなの

## 対策と業界再編

![MCPとA2Aの関係図: MCP = エージェントとツールの接続（手の拡張）、A2A = エージェント同士の通信（同僚との会話）。二層構造を視覚化](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/062_MCPとA2Aの関係図.png)
- 🦜 きなこ：そこで出てきたのが、いくつかの対策と新しいプロトコルなの。まずGoogleが提唱するA2A、Agent-to-Agentプロトコルについて話すね
- 🦜 きなこ：MCPはAIがツールを操作するためのプロトコル。AIの「手」を拡張するイメージ。一方A2AはAI同士が会話して協力するためのプロトコル。AIに「同僚」を作るイメージなの
![二層構造のアーキテクチャ図: 下層「ツールアクセス層: MCP」→ 上層「エージェント間協調層: A2A」。両層をまたぐイベントストリーミング基盤（Kafka等）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/066_二層構造のアーキテクチャ図.png)
- 🦜 きなこ：業界のコンセンサスは「補完的」って見方だよ。MCPでツールに繋ぎ、A2Aでエージェント同士が連携する二層構造になっていくと言われてるの
![各社のスタンスまとめ: AWS「両プロトコル中立サポート」、Google「A2A推進+MCP共存」、Microsoft「Azure API ManagementでMCP認可」、OpenAI「MCP全面採用+独自フレームワーク」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/068_各社のスタンスまとめ.png)
- 🦜 きなこ：AWSはBedrock AgentCoreでMCPもA2Aも両方サポートしてるし、GoogleもGeminiにBYO-MCP機能を入れてMCPとの共存を図ってるの
![AAIF組織図: Linux Foundation傘下にAAIF、その下にMCP（Anthropic寄贈）、goose（Block寄贈）、AGENTS.md（OpenAI寄贈）の3プロジェクト](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/068b_AAIF組織図.png)
- 🦜 きなこ：Linux Foundation配下の新しい財団で、Anthropic、OpenAI、Blockが共同創設した
- 🦜 きなこ：プラチナメンバーにはAWS、Google、Microsoft、Bloomberg、Cloudflareも名を連ねてる

## まとめ

![まとめスライド1: 「MCPの光」月間9700万DL、1万+サーバー、Kubernetes超えの普及速度](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/077_まとめスライド1-MCPの光.png)
- 🦜 きなこ：じゃあ今日のまとめだよ。MCPは月間9700万ダウンロード、1万以上の公開サーバーっていう大成功を収めた
![まとめスライド2: 「MCPの影」CVSS 9.4-9.8の脆弱性多発、Tool Poisoning、Shadow MCP、Anthropic修正拒否](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/078_まとめスライド2-MCPの影.png)
- 🦜 きなこ：でも同時に、標準化が攻撃面を集中させて、CVSS 9点台の脆弱性が次々と見つかった。Tool PoisoningやShadow MCPという新しい脅威も生まれたの
- 🐹 もっちー：便利さと安全は表裏一体ってことだね
![まとめスライド3: 「今後の展望」MCP（ツール層）+ A2A（エージェント層）の二層構造、MCP Gatewayの普及](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V138/080_まとめスライド3-今後の展望.png)
- 🦜 きなこ：今後はMCPとA2Aの二層構造で業界が再編されていく流れだよ。MCPがツールへの接続を、A2Aがエージェント間の協調を担う形

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*