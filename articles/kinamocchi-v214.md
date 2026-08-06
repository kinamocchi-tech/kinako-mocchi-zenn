---
title: 『安い版』のはずが最強に？Gemini 3.5 Flashが変えた常識【解説記事】
emoji: 🤖
type: tech
topics:
- voicevox
- ai
- gemini
- llm
- tech
published: true
---

# 『安い版』のはずが最強に？Gemini 3.5 Flashが変えた常識

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [『安い版』のはずが最強に？Gemini 3.5 Flashが変えた常識](https://www.youtube.com/watch?v=4fG7HB0Ye8g)
:::

## この記事で分かること

- 🐹 もっちー：なあきなこ、Geminiの『Flash』ってさ、安くてしょぼい版のことでしょ？
- 🐹 もっちー：え、うそやん！？安い方が強いってどういうこと？
- 🐹 もっちー：え、それって知らない間に何か買われたりしない？ちょっと怖いんだけど
- 🦜 きなこ：うん、そこはちゃんと後で説明するね。今日はGoogle I/O 2026で発表された内容を、全部つなげて解説するよ

## Gemini 3.5 Flash — 『安いモデル』の看板を破壊した性能

![Diagram of an X mark over a budget-tier icon, replaced below by an upgraded agent-grade engine icon (icon-based, no text)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/012_diagram_x_mark_over.png)
- 🦜 きなこ：そう思うよね。私も最初は、小さなバージョンアップなんだろうって思ってたの。でも中身を見たら完全に別物で、正直びっくりしたんだよ
![Computer Use のスクリーン風図解: AIがブラウザ画面のボタンとカーソルを自分で操作する様子](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/013_computer_use_ai.png)
- 🦜 きなこ：一番大きいのがComputer Use。前は別のモデル扱いだった、パソコンの画面を見て自分で操作する機能が、メインモデルの組み込みツールになったの
- 🦜 きなこ：注文はさせないよ。それに今はまだプレビュー版だから、いきなり全部おまかせできる段階でもないの。そこは私も慎重に見てるの
![API price card for Gemini 3.5 Flash only: input 1.50 dollars and output 9.00 dollars per 1 million tokens. Add two relative comparison labels reading '3x Gemini 3 Flash Preview' and '6x Gemini 3.1 Flash-Lite'. Do NOT show absolute prices for any model other than Gemini 3.5 Flash.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/017_api_gemini_3_5.png)
- 🦜 きなこ：上がったよ。API価格は入力100万トークンで1.50ドル、出力で9.00ドル。前のFlashプレビューのちょうど3倍なの
![Two-panel benchmark card showing Gemini 3.5 Flash own scores only: Terminal-Bench 2.1 at 76.2 percent and MCP Atlas at 83.6 percent. Caption reads 'Surpasses previous flagship Gemini 3.1 Pro'. Do NOT show any numeric score for Gemini 3.1 Pro.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/019_terminal_bench_2_1.png)
- 🦜 きなこ：そこが面白いの。コーディングとエージェントの指標で、Terminal-Bench 2.1が76.2%、MCP Atlasが83.6%。前世代の最上位を超えたの
![Bar chart comparing MCP Atlas benchmark scores: Gemini 3.5 Flash 83.6% / Claude Opus 4.8 82.2% / GPT-5 44.5%, with a small speed icon indicating roughly 4x output speed](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/021_bar_chart_comparing_mcp.png)
- 🦜 きなこ：同じMCP Atlasで、Claude Opus 4.8が82.2%、GPT-5が44.5%。しかも他のモデルの約4倍の速さで動くの

## 料金の大改編 — Ultra値下げ・Developer tier新設・コンピュート課金

- 🦜 きなこ：そう思うよね。実は私も最初は、素直に安くなったって思ったの。でもね、発表された数字をぜんぶ並べてみたら、見え方がまるっきり変わったんだよ
![Price drop diagram: Gemini Ultra monthly $250 to $200 with a down arrow (icon-based, no on-screen text)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/025_price_drop_diagram_gemini.png)
- 🦜 きなこ：まず事実から。最上位のGemini Ultraが、機能はそのままで月額250ドルから200ドルへ値下げされたの。期間限定じゃなくて恒久的な改定なんだよ
![Developer tier（月額99.99ドル）と Ultra（月額200ドル）の比較表を段階表示（利用枠5倍・20TBストレージを併記）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/027_developer_tier_99_99.png)
- 🦜 きなこ：そこなんだよ。だから今回、新しく月額99.99ドルのDeveloper tierが新設されたの。Proの5倍の利用枠と、20TBのクラウドストレージが付くんだよ
- 🦜 きなこ：そういうこと。250ドルは高すぎて手が出なかった個人開発者やクリエイターを、ちょうど拾える段の値段なの。YouTube Premiumまでバンドルされてるんだよ
![課金の物差しの変化を対比図で表示（旧: プロンプト回数カウント ⇔ 新: 計算量（コンピュート）カウント）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/030_cue.png)
- 🦜 きなこ：でもね、私が本当に唸ったのは値段じゃないの。利用制限の数え方が、プロンプト回数から計算量ベースへ、物差しごとまるごと変わったんだよ。ここが一番大きい
![利用枠リセット間隔 24時間→5時間の短縮を時計アイコンで対比表示（軽いタスクは消費小・重いエージェント作業は消費大）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/032_24_5.png)
- 🦜 きなこ：軽いテキスト質問の消費は小さくなったの。ただ、利用枠のリセット間隔は24時間から5時間へ短縮されたから、重いエージェント作業ほど計算量を食べる仕組みになったんだよ

## 『買収』と呼ばれない買収 — Contextual AIアクハイアの正体

![Side-by-side comparison diagram: M&A corporate acquisition icon vs. license contract plus talent-transfer arrow icon (acquihire), icon-based without on-screen text](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/034_side_by_side_comparison.png)
- 🦜 きなこ：そこで引っかかったの、すごく正しいんだよ。実はそこ、Googleが意図的に選んだ抜け道なの。だからニュースでも、買収とは書かれてないの
![Google DeepMind と Contextual AI のライセンス契約 約8,000万〜9,000万ドル（$80-90M）を金額カードで表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/035_google_deepmind_contextual_ai.png)
- 🦜 きなこ：今回Google DeepMindがやったのは、Contextual AIと約8000万から9000万ドルのライセンス契約を結ぶことだったの
![Talent flow diagram: left card labeled 'Contextual AI', right card labeled 'DeepMind', connected by a right-pointing arrow, with a caption reading 'Douwe Kiela and 20+ researchers'. Use plain text name labels and generic abstract shapes only — no company logo, wordmark or brand mark of any kind.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/036_douwe_kiela_20_contextual.png)
- 🦜 きなこ：そしてそのライセンス契約と同時に、CEOのDouwe Kielaを含む20名以上の研究者が、そろってDeepMindの中に移ってるの
![書類上の構造（技術ライセンス契約＋個人の転職）と実態（組織まるごと移転）の二層対比図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/038_cue.png)
- 🦜 きなこ：中身はほとんどそうなの。でも書類の上では、会社を買ったんじゃなくて、技術を貸し借りして、人が個人で転職しただけっていう形になってるんだよ
![M&A なら反トラスト審査あり／アクハイアなら審査の入り口に乗らない、を分岐フロー図で表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/039_m.png)
- 🦜 きなこ：この形だと企業買収として扱われないから、アメリカとEUの厳しい独占禁止法の審査に、そもそも入り口から乗らないの。審査で止められる心配も、そこで消えるの
![Contextual AI は独立法人として存続。Character.AI・Hume AI の同型事例を並列表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/041_contextual_ai_character_ai.png)
- 🦜 きなこ：しかもContextual AIは、今もちゃんと独立した会社として残ってるの。Character.AIやHume AIの時と、同じやり方なんだよ

## 24時間稼働のエージェント『Spark』——便利さと危うさ

![閉じたノートPCの隣で、カレンダーの予定が自動で埋まっていくイメージ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/043_pc.png)
- 🦜 きなこ：ちょっと想像してみて。ノートPCを閉じて出かけたのに、帰ってきたら会議の日程調整が全部終わってるの。誰も触ってないのに、勝手に全部進んでるんだよ
![Google Cloud上の専用仮想マシンがユーザーのPCと切り離されて稼働している構成図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/045_google_cloud_pc.png)
- 🦜 きなこ：動いてるのはあなたのPCじゃないの。Google Cloud上の専用の仮想マシンが、あなたの代わりに黙々と作業を続けてるんだよ。だからPCの電源も関係ないの
![「Gemini Spark」の名称カードを表示（24時間365日稼働のパーソナルAIエージェント）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/047_gemini_spark_24_365.png)
- 🦜 きなこ：そう、24時間365日ずっと。実はこの子、ちゃんと名前がついてるの。Gemini Spark。あなたの代わりに動き続ける常時稼働のエージェントだよ
![Sparkが自律実行するタスク例をフロー図で表示（メールの要約 → イベントの計画調整）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/049_spark.png)
- 🦜 きなこ：やることは意外と地味なんだけどね。メールの要約とか、イベントの計画の調整みたいに、複数ステップにまたがる作業を、人の手を借りずに順番に進めていくの
![Chromeブラウザ内でSparkがクリック・データ入力を代行するイメージ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/050_chrome_spark.png)
- 🦜 きなこ：しかもChromeブラウザの中でも直接動く予定で、ウェブ上のクリックやデータ入力まで、あなたの指示のもとで代わりにやってくれるの
![Three-layer defense stack diagram for Spark: layer 1 labeled AP2, layer 2 labeled OAuth2 scope control, layer 3 labeled Approval Gate](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/052_three_layer_defense_stack.png)
- 🦜 きなこ：そこは私も最初に引っかかったところ。だからSparkには、資金の意図しない消費や大事なデータの流出を防ぐ歯止めが、三段構えで入ってるの

## キーボードからの解放 — Workspace音声統合（Gmail/Docs/Keep Live）

![Gmail Live・Docs Live・Keep Liveの3機能を3枚のカードで並べて表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/058_gmail_live_docs_live.png)
- 🦜 きなこ：そう思うよね。私も最初はそう思ってたの。でもGmail Liveに今週の学校行事は？って聞くと、メールの履歴から答えが音声で返ってくるんだよ
![キーワード検索（該当メールを一覧表示）とGmail Live（文脈を理解して答えを生成）の対比図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/060_gmail_live.png)
- 🦜 きなこ：そこが決定的に違うの。大量のメール履歴を横断して文脈を読んで、探すんじゃなくて答えまで作ってくれるんだよ。文字起こしとは別物なの
![Docs Live: 口頭のアイデア羅列 → AIが構成整理 → Drive/Gmailから関連情報を抽出 → 初稿ドラフト完成の4ステップ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/062_docs_live_ai_drive.png)
- 🦜 きなこ：Docs Liveはもっと踏み込むよ。とりとめなく話したアイデアをAIが構成に整理して、許可した範囲でDriveやGmailから材料も集めて初稿を作るの
![Keep Live: 雑多な音声メモがギフト案・買い物リスト・リフォーム計画のリストへ自動分類される様子](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/064_keep_live.png)
- 🦜 きなこ：Keep Liveも面白いよ。ギフトのアイデアも買い物リストもリフォームの計画も、続けて話すだけでトピックごとに自動で分類されて残るの
![展開スケジュール: 2026年夏よりGoogle AI Pro/Ultra契約者とWorkspaceビジネスユーザー（プレビュー版）へ提供](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/065_2026_google_ai_pro.png)
- 🦜 きなこ：展開は2026年夏から。まずGoogle AI Pro/Ultraの契約者と、Workspaceのビジネス向けプレビューが対象なんだよ
- 🐹 もっちー：声のスピードで仕事するって聞いたけど、ぼく想像つかないんだけど。結局しゃべって、文字に起こして終わりでしょ？それ、前からあるやつだよね？

## 9億MAUと収益の3本柱 — なぜGoogleは『廉価版』に本気を出せたのか

- 🦜 きなこ：そう思うよね。私も最初はそう見てたの。実際ChatGPTは月間10億人で、Geminiアプリは9億人。数字だけなら、たしかに負けてるんだよ
![収益3本柱の図解: 検索広告（無料ユーザー）／Workspace 課金（ナレッジワーカー）／Google Cloud・Vertex AI（開発者・企業）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/071_3_workspace_google_cloud.png)
- 🦜 きなこ：そこが一番おもしろいところなの。Googleの回収は柱が3本あるんだよ。無料の人からは検索広告、働く人からはWorkspaceの課金、開発者と企業からはGoogle Cloud
![棒グラフ: 2026年Q1 Google Cloud 売上200億ドル・前年同期比63%増、生成AI プロダクト収益は前年比約800%増](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/072_2026_q1_google_cloud.png)
- 🦜 きなこ：数字で見ると分かりやすいよ。2026年第1四半期のGoogle Cloudの売上は、前年同期比63%増の200億ドル。生成AI関連の収益は前年比で約800%増なの
- 🦜 きなこ：そこなんだよ。最初にもっちーが聞いてたよね。なんでGoogleがそこまで本気になれたのか。答えは売上の大きさだけじゃなくて、コストの方にあったの
![グラフ: ハードウェア（第8世代TPU）とソフトの協調設計による推論コスト前年比78%削減と、Flash への投資を結ぶ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/075_8_tpu_78_flash.png)
- 🦜 きなこ：第8世代TPUとソフトの協調設計で、推論コストを前年比78%も削れたの。だから廉価版に見えるFlashにまで、あれだけ本気で投資できたんだよ
- 🐹 もっちー：ほら見ろ！やっぱりChatGPTの勝ちやん！Googleは検索で天下取ったのに、AIでは二番手ってことやろ？ワイでも分かる話やで！

## 競合との住み分けと、数学の未解決問題を解いたAI

![4社の戦略ポジショニングマップ表示（Google=OSレイヤー統合／OpenAI=タスク自動化／Anthropic=プロジェクトRAG／Meta=オープンウェイト）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/077_4_google_os_openai.png)
- 🦜 きなこ：その感覚は大事だよ。でもね、そこまで踏み込んでるのはGoogleだけで、OpenAIもAnthropicもMetaも、それぞれ全然違う方向から日常の自動化を狙ってるの
![Anthropic Claude Projects の図解: 長期メモリ＋自律ブラウジングで特定テーマ（競合ニュース追跡）をプロアクティブに情報提供](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/080_anthropic_claude_projects.png)
- 🦜 きなこ：AnthropicのClaude Projectsは長期メモリ型。競合ニュースの追跡みたいに、ひとつのテーマを自分で調べ続けて先に教えてくれるのが強みって言われてるの
![Meta Llama 4 の図解: オープンウェイトを自社インフラに閉じて推論。GDPR/HIPAA準拠のデータ主権を求める医療・金融のオンプレ展開](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/082_meta_llama_4_gdpr.png)
- 🦜 きなこ：そう、Llama 4はオープンウェイト。データを社外に出せない医療や金融みたいな規制産業が、自社のサーバーの中だけで動かせるのがいちばんの狙いなの
![データの重力の概念図: Gmail・カレンダー・Android・Workspaceという個人データ基盤が中心にあり、Geminiがネイティブ権限でその上に乗る構造](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/084_gmail_android_workspace_gemini.png)
- 🦜 きなこ：データの重力なの。GmailもカレンダーもAndroidも、みんながもう使ってる場所にGeminiがいるから、外部のAPIを叩かなくてもそのまま生活に入ってこれるの
![Achievement panel for Aletheia with three cards: 'Erdos-1051 autonomously solved', 'FirstProof 6 of 10 problems', 'IMO-ProofBench about 91.9 percent'. Crisp sharp text rendering, no blur or ghosting.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/085_aletheia_erd_s_1051.png)
- 🦜 きなこ：そのGoogleのDeepMindが、Aletheiaで数十年解けなかったエルデシュ問題を自力で解いて、IMO-ProofBenchでも91.9%を出したの
![Flowchart: proof generation, self-verification loop, and a stop icon shown when a proof cannot be verified (icon-based, no on-screen text)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/087_flowchart_proof_generation_self.png)
- 🦜 きなこ：でもね、Aletheiaで一番すごいのは解けたことじゃないの。解けないときは答えをでっちあげずに、正直に失敗を認める。だから結果を信じられるんだよ

## まとめ

![Summary slide with five numbered cards labeled 'Flash Performance', 'Pricing Revision', 'Talent Acquisition', 'Spark Always-On', 'Voice Integration'. Use abstract geometric icons only — represent 'Talent Acquisition' with a transfer-arrow icon, never with human figures or person pictograms.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/088_5_flash_spark_1.png)
- 🦜 きなこ：じゃあ今日の話をまとめるね。Flashの性能アップ、料金体系の改編、買収を装わない形での人材の獲得、Sparkの常駐化、そして音声の統合
- 🐹 もっちー：バラバラのニュースだと思ってたけど、そう考えるとGoogleって、単にAIを作ってるだけじゃないんだな。生活のほうにAIを溶け込ませにきてるんだ
- 🦜 きなこ：そこなの。モデルを強くして、値段を下げて、人と技術を集めて、エージェントを常駐させて、声でつなぐ。全部、AIを意識しないで使える環境を作るための一手なんだよ
![Bookmark or save icon badge overlay (icon-based, no on-screen text)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V214/091_bookmark_save_badge_overlay.png)
- 🐹 もっちー：ワイ、この5つの流れは保存版やな！あとで絶対見返すで。…そういやきなこ、飼い主のタブレットの充電だいぶ減ってるけど、気づかれへんか？

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*