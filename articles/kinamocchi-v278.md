---
title: MCPサーバー自作は簡単？でも認証の3つのMUSTは外せない【解説記事】
emoji: 🐹
type: tech
topics:
- ai
- llm
- tech
published: true
---

# MCPサーバー自作は簡単？でも認証の3つのMUSTは外せない

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [MCPサーバー自作は簡単？でも認証の3つのMUSTは外せない](https://www.youtube.com/watch?v=-fIE-Vsh-A0)
:::
@[youtube](-fIE-Vsh-A0)

## この記事で分かること

- 🦜 きなこ：無理もないよ、公式が正式に発表したのはつい先月のことだから。ここからじっくり中身を一緒に見ていこうね
- 🐹 もっちー：根っこから変わったってことだよね？それって結構大きな話じゃん
- 🐹 もっちー：3つのMUST…？なんか怖い響きやん
- 🦜 きなこ：その勘、悪くないよ。実装が簡単になった分、しわ寄せは認証のところに全部寄せられてるの。だから今日はそこを一番の重点にして丁寧にやっていくね

## 仕様の中身、実は別物になっていた

![Version timeline telop: 2025-11-25 (previous stable) then 2026-07-28 (latest), caption reads MCP versions are dated, not numbered](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/018_version_timeline.png)
- 🦜 きなこ：ムダじゃないよ。まずね、MCPの仕様はバージョンが数字じゃなくて日付で管理されてるの。前の安定版が2025年11月25日で、いまの最新が2026年7月28日なんだよ
![Old handshake sequence diagram with initialize/initialized exchange and the Mcp-Session-Id header struck through in red](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/020_session_id_struckthrough.png)
- 🦜 きなこ：いつ時点の話かが一発で分かるの。それでね、この7月28日版で、イニシャライズっていう最初の握手と、セッションIDを持ち歩くヘッダが、どっちもきれいに廃止されたんだよ
![Quote card from the official MCP blog: MCP is transforming from a bidirectional stateful protocol into a request/response stateless protocol](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/022_official_blog_quote.png)
- 🦜 きなこ：気持ちは分かるよ。公式ブログにはね、双方向でステートフルなプロトコルから、リクエストとレスポンスのステートレスなプロトコルへ変わる、ってはっきり書いてあるの
![New diagram: a single stateless request and response pair, with a crossed-out session store icon beside the server](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/024_stateless_diagram.png)
- 🦜 きなこ：近いね。前は最初に握手して、そのやり取りの続きをずっと覚えててもらってたの。今は一回のお願いだけで話が完結するから、そもそも覚えててもらう必要がないんだよ
![Load balancer diagram: round-robin arrows distributing requests to three identical server instances, labels read no sticky routing and no shared session store](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/026_load_balancer.png)
- 🦜 きなこ：そう、その手間の代わりに大きな得があるの。同じ機械に戻らなくてよくなるから、順番にぐるっと配るだけでよくて、どのサーバーが受け取ってもちゃんと動くんだよ
- 🦜 きなこ：そこは大丈夫、まるっと一年の移行期間つきなの。ここまでで仕組みが変わったのは分かったよね。でも実装のハードルまで下がったって話は、実はもっと意外なの

## 型注釈だけでtoolになる — 最小実装

![Install card: pip install "mcp[cli]" command with an official Python SDK badge and a Python 3.10+ requirement chip](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/032_pip_install_card.png)
- 🦜 きなこ：じゃあ実物を見せるね。公式のPython SDKはmcpってパッケージで、Python 3.10以上あればすぐ始められるんだよ
![Before/after split: left side shows a dense hand-written JSON Schema block, right side shows a short Python function](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/034_before_after_schema.png)
- 🦜 きなこ：その理解で合ってるよ。今までその一覧のために、JSON Schemaって仕様書を手で書いてたんだよ
![Code snippet with the @mcp.tool() decorator line highlighted directly above a plain Python function definition](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/036_mcp_tool_decorator.png)
- 🦜 きなこ：書かなくていいの。関数の上に@mcp.tool()って一行足すだけ。解析コードも検証コードも一行も要らないんだよ
- 🦜 きなこ：近いかも。関数に「これはtoolだよ」って目印を貼るだけの一行。中身は普段書いてるPythonのままでいいんだよ
![Full minimal snippet on screen: @mcp.tool() on one line, def add(a: int, b: int) -> int on the next, nothing else](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/040_minimal_snippet.png)
- 🦜 きなこ：公式READMEの例だとこう。@mcp.tool()の次の行に def add(a: int, b: int) -> int。これだけで終わりなんだよ
- 🦜 きなこ：呼べるの。この一行が付いてるだけで、普通の関数の三か所がAIから見える形へ自動的に変換されて登録されるんだよ

## 簡単さの裏にある3つのMUST

![Title card in dark red: MCP authorization, the part everyone skips. Small warning triangle icon beside the text](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/053_authorization_title.png)
- 🦜 きなこ：もっちー、鋭いね。正直に言うとね、私も最初は認可の章を後回しにしてたの。あとで読めばいいって見立てが甘かったんだよ
![Clean diagram card: OAuth 2.1 logo-style label at center, subtitle Model Context Protocol authorization is built on OAuth 2.1](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/055_oauth21_diagram.png)
- 🦜 きなこ：そう、ここが今日いちばん大事なところ。関数一個で動くからこそ、認証を素通りさせやすいの。MCPの認可はOAuth 2.1がベースなんだよ
![Bold red telop MUST filling the frame, then three numbered slots appear underneath, still blank](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/059_must_telop.png)
- 🦜 きなこ：そのうえで公式は、大文字のMUSTで「絶対に守れ」って条件を三つ置いてるの。ここを外した瞬間に事故になる、いちばん危ないポイントだよ
![Quote card with the spec sentence MCP servers MUST NOT accept any tokens that were not explicitly issued for the MCP server, the words MUST NOT highlighted in red](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/061_quote_must_not.png)
- 🦜 きなこ：一つ目はトークンのパススルー禁止。仕様の原文は「自分に発行されたトークン以外を受け取ってはならない」なの。MUST NOTだよ
![Three-stage flow: Client sends token A to MCP server, MCP server discards token A and sends a different token B to the internal API, a red X marks the arrow that would pass token A straight through](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/063_three_stage_flow.png)
- 🦜 きなこ：まさにそれ。社内APIを叩くときは、クライアントの鍵をそのまま渡さず、上流の認可サーバーが発行した別のトークンを使わないといけないの
![Two error cards side by side: left card labeled Tool-level error showing isError true with a text content block, right card labeled Protocol-level error showing JSON-RPC codes -32601 and -32602](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/065_error_cards.png)
- 🦜 きなこ：弾いたあとの作法も決まってるの。ツール側の失敗はisErrorってフラグと理由の文章で返して、知らないツールを呼ばれたらJSON-RPCのエラーコードで返すんだよ

## Claude Codeに繋いで、社内ツールに広げる

![Terminal-style card typing out the command: claude mcp add my-server -- python server.py, cursor blinking](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/076_terminal_claude_mcp_add.png)
- 🦜 きなこ：そこはね、拍子抜けするくらいあっさりなの。ターミナルを開いて claude mcp add って打つ。それだけで終わりなんだよ
![Split card: LEFT Local server = stdio (default, no flag) with a laptop icon](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/078_split_local_server.png)
- 🦜 きなこ：重いのは中身を守る話で、繋ぐ作業そのものは軽いの。自分のパソコンで動かすなら、stdioが既定だから指定もいらないんだよ
- 🦜 きなこ：そう、よく覚えてたね。だから最初の一歩に向いてるんだよ
![Same split card completed: RIGHT Hosted server = --transport http with a cloud icon](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/082_split_hosted_server.png)
- 🦜 きなこ：そこはURLで届くホスト型だから、--transport httpを足すの。公式ドキュメントに例があるから書き換えれば大丈夫
![Debug tool card: npx @modelcontextprotocol/inspector, three mode chips labeled Web UI / CLI / TUI, footnote requires Node.js >= 22.19.0](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/084_inspector_debug_card.png)
- 🦜 きなこ：公式のMCP Inspectorがあるの。npxで起動すれば、Web画面・コマンド・端末表示の三通りで中身を覗けるよ
![Reference-implementation card: modelcontextprotocol/servers listing Git / Filesystem / Memory, beside Microsoft's PostgreSQL MCP sample repository](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/086_reference_implementations.png)
- 🦜 きなこ：公式のサーバー集が手本になるの。MicrosoftもPostgreSQL接続の見本を、権限の扱いごと公開してるんだよ

## まとめ

![digest recap: stateless diagram, minimal code snippet, 3 MUSTs card, connection patterns](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/095_ending_digest_recap.png)
- 🦜 きなこ：今日の話を振り返ってまとめると、MCPはステートレス化・SSE非推奨・認可の強化っていう大きな3つの変化を経てるんだよ
- 🐹 もっちー：難しそうって思ってたけど、まず動かすだけならワイでもできそうやな
- 🦜 きなこ：その気持ちが一番大事なんだよ。難しそうに見えても、実際に自分の手を動かしてみると理解の速度が全然変わってくるから
![terminal cut: npx @modelcontextprotocol/inspector](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V278/098_ending_terminal_cut.png)
- 🦜 きなこ：そう思ってくれたなら、今日からできる一歩があるの。コマンド1個打つだけだから

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*