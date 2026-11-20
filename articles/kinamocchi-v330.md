---
title: Gemini APIのツール定義は後から読める。Tool Retrieval（preview）解説【解説記事】
emoji: 🤖
type: tech
topics:
- voicevox
- ai
- gemini
- geminiapi
- toolretrieval
published: true
---

# Gemini APIのツール定義は後から読める。Tool Retrieval（preview）解説

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [Gemini APIのツール定義は後から読める。Tool Retrieval（preview）解説](https://www.youtube.com/watch?v=3GGQAPpJECQ)
:::
@[youtube](3GGQAPpJECQ)

## この記事で分かること

![冒頭カード：Gemini API / Tool Retrieval](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/001_visual.png)
- 🐹 もっちー：ねえきなこ、AIにツールを何百個もつなぐと、毎回その説明を全部読ませるから、重くなるでしょ？
- 🐹 もっちー：えっ、全部読ませんでええようになるん！？ どういう仕組みなん？
- 🐹 もっちー：それやったら速くなりそうやん！ ほんまに何でも軽くなるん？

## Tool Retrievalとは、何が困っていたのか

![用語: ツール＝名前＋説明＋引数のschema](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/012_visual.png)
- 🦜 きなこ：AIエージェントは、検索や返金みたいな関数を、ツールとして呼び出すの。ツール1つごとに、名前と説明と、引数の形を決めたschemaがあるよ
![図: schema＝入力の設計図（例: order_id と amount）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/014_visual.png)
- 🦜 きなこ：『この関数には、注文番号と金額を入れてね』みたいな、入力の形を書いた設計図のこと。ツールが増えるほど、この設計図も増えるよ
![テロップ: 課題＝入力トークン増／レイテンシ増／ツール選択の精度低下（Google発表）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/015_visual.png)
- 🦜 きなこ：Googleの発表では、数十個、場合によっては数百個のツールにつながると、全部のschemaをモデルのコンテキストに載せることになって、入力トークンとレイテンシが増えるの
- 🦜 きなこ：ツールを選ぶ精度も下がる、と説明されてるよ
- 🦜 きなこ：いい例えだね。Tool Retrievalは、メニューには料理名と一言だけ載せて、レシピは注文が入ってから出すイメージなの
![イメージ（擬似コード・公式サンプルの構成を省略）: tools=[{"type":"tool_search"}, {…, "defer_loading": true}]](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/020_visual.png)
- 🦜 きなこ：リクエストにtool_searchっていうツールを足して、後回しにしたいツールにdefer_loadingをtrueにするの

## キャッシュ、MCP、クライアント側検索

![図: 先頭＝変わらない／読み込んだschemaは後ろに追加](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/031_visual.png)
- 🦜 きなこ：発表では、相性がいいって書いてあるの。後回しにしたschemaは、プロンプトの先頭に出ないでしょ
- 🦜 きなこ：読み込んだものは会話の後ろに足されるから、キャッシュされる先頭部分が、毎ターン変わらないの
- 🦜 きなこ：次はMCP。外部のサービスにつなぐ仕組みで、1つのMCPサーバーが、たくさんのツールを持つことがあるの
![テロップ: mcp_serverにdefer_loading → 全ツールがオンデマンド](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/035_visual.png)
- 🦜 きなこ：リモートMCPサーバーのツール定義にdefer_loadingをtrueにすると、そのサーバーのツール全部が、必要な時だけの読み込みになるの
- 🦜 きなこ：大きなサーバーも、schemaを1個ずつ載せずにつなげるよ。名前と説明は載るけどね
![用語: クライアント側検索＝検索を自分のアプリで実行（execution: client）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/038_visual.png)
- 🦜 きなこ：その時のために、クライアント側の検索もあるの。tool_searchにexecutionをclientで宣言して、検索の中身は自分のアプリで作るの

## 料金と対応モデル

![テロップ: 専用の追加料金なし（標準トークン料金）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/047_visual.png)
- 🦜 きなこ：Tool Retrieval専用の追加料金はないの。使ったトークンが、呼び出したモデルの標準料金で数えられるよ
- 🦜 きなこ：必ずとは言えないの。tool_searchをオンにすると、小さな固定の入力が加わるよ
- 🦜 きなこ：それに、読み込んだschemaは、そのあとの会話でも入力として数えられるの。最初から宣言した時と同じ扱いね
![テロップ: 減る条件＝使わないschema ＞ 読み込むschema（発表: 自分のトラフィックで測定を）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/051_visual.png)
- 🦜 きなこ：減るのは、使わないschemaのほうが、読み込んだschemaより多い時なの
- 🦜 きなこ：大きなツール一覧なら普通はそうだけど、自分のトラフィックで測ってね、って発表にも書いてあるよ
![テロップ: deferredツール1つ＝入力に1行（初期テストで約26トークン／ドキュメント）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/054_visual.png)
- 🦜 きなこ：ドキュメントには、もっと細かい点もあるの。後回しにしたツールも、1つにつき名前と説明の1行が、入力に載るの

## previewの注意点と、他社の似た機能

![テロップ: preview＝GA前に変更の可能性／Interactions APIのみ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/067_visual.png)
- 🦜 きなこ：ドキュメントには、previewで、一般提供の前にAPIの形が変わる可能性がある、と書いてあるの
- 🦜 きなこ：それと、使えるのはInteractions APIだけで、従来のgenerateContentでは使えないよ
![表: tool_search＝1リクエストに1つ／サーバー側とクライアント側は混在不可](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/069_visual.png)
- 🦜 きなこ：決まりごとも幾つかあるよ。tool_searchは、1リクエストに1つだけ。サーバー側とクライアント側は、同じリクエストで混ぜられないの
![テロップ: 読み込んだツールは外せない／ツール宣言は毎回すべて送り直し](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/071_visual.png)
- 🦜 きなこ：外せないの。読み込んだツールは、会話が続く間ずっとコンテキストに残るよ。それと、ツールの宣言は保存されないから、毎回toolsの全体を送り直すの
- 🦜 きなこ：発表が言ってるのは、モデルが読む量を軽くする話なの。APIへの送信量が減るかどうかは、今回の資料では言えないよ
![テロップ: tool_search_call／tool_search_result は署名ごと変更せず送り返す](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/075_visual.png)
- 🦜 きなこ：もう一つ。会話を自分で管理する時は、tool_search_callとtool_search_resultのステップを、署名もそのまま送り返す必要があるの

## まとめ

![まとめ: ①必要な時だけschemaを読み込む ②専用の追加料金なし・必ず安くなるとは限らない ③preview・制限あり](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/089_visual.png)
- 🦜 きなこ：まとめるね
- 🦜 きなこ：Tool Retrievalは、ツールの中身を必要な時だけ読み込んで、入力を軽くしようとする、Gemini APIのpreview機能なの
- 🐹 もっちー：専用の追加料金はないけど、必ず安くなるわけじゃない、が大事だよね
![テロップ: 出典＝公式ブログ／AI Studioドキュメント／Anthropicドキュメント（概要欄）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V330/093_visual.png)
- 🦜 きなこ：対応モデルと制限は、ドキュメントで最新を確認してね。数字の出どころは、概要欄に公式のリンクを貼ったよ
- 🐹 もっちー：それ、名前と一言の説明だけ見えとったら助かるやつやん！ ほな、投げ銭より先に、整理からやな！ あなたのエージェントには、ツールが何個ある？ コメントで教えてね

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*