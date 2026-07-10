---
title: ブラウザ操作AIはオワコン？Project Mariner終了とAPIファースト【解説記事】
emoji: 🤖
type: tech
topics:
- mcp
- ai
- voicevox
- llm
- tech
published: true
---

<!-- グラレコ:graphreco -->
![ブラウザ操作AIはオワコン？Project Mariner終了とAPIファースト【解説記事】｜グラレコ要約](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/V158_graphreco.png)

# ブラウザ操作AIはオワコン？Project Mariner終了とAPIファースト

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [ブラウザ操作AIはオワコン？Project Mariner終了とAPIファースト](https://www.youtube.com/watch?v=LwsaqaMOwSA)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、AIエージェントって、ブラウザを目で見てポチポチ操作するやつでしょ？
- 🐹 もっちー：えーっ！Googleが諦めたって、どういうこと？！
- 🐹 もっちー：プロジェクト・マリナー...なんか冒険家みたいな名前やけど、それが終わったの？
- 🦜 きなこ：ブラウザを目で見て操作するAIから、コードとAPIで動くAIへ。今日はその理由と未来を解説するね

## mariner_end

- 🦜 きなこ：まずProject Marinerとは何だったか、おさらいするね
![Project Marinerの仕組み：スクリーン→AI→マウス・キーボード操作の図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/013_mariner_mechanism.png)
- 🦜 きなこ：そう。スクリーンショットを見てリアルタイムでウェブサイトをマウス・キーボードで自動操作するAIエージェントなの
- 🦜 きなこ：オンラインショッピング・情報検索・フォーム入力みたいな複数ステップのタスクを自動化できたの
![タイムライン：2024年10月開始→2026年3月スタッフ再配置→2026年5月終了](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/017_mariner_timeline.png)
- 🦜 きなこ：2026年3月ごろから、Wiredの報道でMarinerチームからスタッフが再配置されてるって判明したの
- 🦜 きなこ：そう。そして2026年5月4日に正式終了。Googleは『MarinerのテクノロジーはGoogle製品に航海した』と発表したんだよ
- 🦜 きなこ：要するに、技術はGemini APIや新しいGemini Agentに吸収されるってこと

## browser_limits

- 🦜 きなこ：次に、なぜブラウザ操作型AIが難しかったか、技術的な限界を解説するね
![DOM解析 vs スクリーンショット解析の比較図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/031_dom_vs_screenshot.png)
- 🦜 きなこ：まずDOM解析と視覚的スクリーン解析の話から。DOM解析って覚えてる？
- 🦜 きなこ：ウェブページの構造データのことだよ。DOMにアクセスできれば、精度が圧倒的に高くて処理も軽いの
- 🦜 きなこ：DOMが取れないサイトがあるから。JavaScriptが大量にレンダリングするサイトだとDOMに直接アクセスできないんだよ
- 🦜 きなこ：そこが問題でね。ページ上の誤った要素を選択するエラーが頻発したの。ボタンを誤クリックしたり
![CAPTCHAブロックの図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/039_captcha_block.png)
- 🦜 きなこ：視覚処理は計算コストも高くてね。それだけじゃなくて、CAPTCHA問題もあるんだよ

## code_first

- 🦜 きなこ：じゃあAPIファーストの何がそんなに強いの？具体的に見ていくね
![Claude Code vs OpenAI Codex 比較表（SWE-bench・トークン効率・速度）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/056_claude_vs_codex_comparison.png)
- 🦜 きなこ：まずコード品質から。SWE-benchというソフトウェアエンジニアリングベンチマークで比較すると、Claude Code（Opus 4.7）は開発者の盲検評価で67%勝利しているの
- 🦜 きなこ：どちらがより良いコードか人間が判断する実験で、3回に2回はClaude Codeが選ばれるってこと
- 🦜 きなこ：Codexは150万トークン/タスクで高速。Claude Codeは626万トークン使うけど、アーキテクチャ推論と長コンテキストが強いの
- 🦜 きなこ：そう。2026年のベストプラクティスは、アーキテクチャ重視ならClaude Code、スコープ明確で高速実装ならCodexという使い分けなんだよ
![APIファースト4つの強み：安定性・速度・保守性・監査性](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/064_api_first_4_strengths.png)
- 🦜 きなこ：4つの強みがあって。安定性——UI変更に非依存。速度——読み込み遅延なし。保守性——インターフェース変更の影響最小。監査性——APIログで完全追跡できるの

## computer_use

- 🦜 きなこ：じゃあブラウザ操作型は完全に終わりなの？って気になるよね
![OpenAI Operatorの現状：Early research preview・段階展開](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/084_openai_operator_status.png)
- 🦜 きなこ：まずOpenAI Operator。2026年5月時点でまだEarly research preview——ChatGPT Plus/Team向けに段階展開中なの
- 🦜 きなこ：OSWorldベンチマークで38.1%の達成率で、月次で向上してるの。スライドショー作成やカレンダー管理はまだ苦手なんだよ
![Anthropic Computer Use：保険業務94%達成](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/088_computer_use_insurance.png)
- 🦜 きなこ：Anthropic Computer UseはSonnet 4.6・Opus 4.7で使えるの。保険業務のベンチマークで94%を達成してるんだよ
- 🦜 きなこ：保険業務みたいな特定の業務には強いの。でも汎用ブラウザ操作はまだ発展途上なんだよ
![コンピューター操作型AIの残存用途4つ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/092_remaining_use_cases_4.png)
- 🦜 きなこ：4つの残存用途があるの。1つ目がAPIが非公開のレガシーシステム——DOM解析もAPI連携も不可能な古いシステムの操作

## market_2026

- 🦜 きなこ：最後に2026年Q2のAIエージェント市場の勢力図を整理するね
![AIエージェント市場3セグメント図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/103_agent_market_3segments.png)
- 🦜 きなこ：そう。セグメント①がコード生成・開発者向け——Claude Code・OpenAI Codex・Google Antigravity CLI
- 🦜 きなこ：CursorはARRが20億ドルに達したと言われてるの。ただし二次ソースの情報だから確認が必要なんだけどね
![市場成長グラフ：$128億（2026）→$301億（2032）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/107_market_growth_chart.png)
- 🦜 きなこ：AIコーディングツール市場は2026年の128億ドルから2032年に301億ドルへ、年間成長率27%で拡大すると予測されてるの
![セグメント②：GUI自動化型の各プレイヤー比較](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/109_segment2_gui_players.png)
- 🦜 きなこ：セグメント②がGUI自動化・Computer Use型。Anthropic Computer Use・OpenAI Operator・Apple Siri 2026があるの
- 🦜 きなこ：Siri 2026はマルチステップインテントとクロスアプリ連携ができるようになってるの。Google Geminiとも統合してる

## まとめ

![まとめスライド](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V158/120_summary_slide.png)
- 🐹 もっちー：今日めっちゃ勉強になった！まとめると？
- 🦜 きなこ：Project Mariner終了は偶然じゃなくて、業界全体の転換を先取りしてたの
- 🦜 きなこ：ポイントは3つ。1つ目、ブラウザ操作型AIは精度・CAPTCHA・セキュリティの三重苦で行き詰まった
- 🦜 きなこ：2つ目、Claude Code・MCPなどコードファースト・APIファーストのアプローチが市場を支配した

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*