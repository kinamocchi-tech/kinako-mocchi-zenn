---
title: Googleは遅れてる？Cloud Next '26が証明した企業AI支配の実態【解説記事】
emoji: 🤖
type: tech
topics:
- tpu
- ai
- mcp
- llm
- tech
published: true
---

# Googleは遅れてる？Cloud Next '26が証明した企業AI支配の実態

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [Googleは遅れてる？Cloud Next '26が証明した企業AI支配の実態](https://www.youtube.com/watch?v=rzWdjWvC28M)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、最近みんな「Googleって遅れてるよね」って言ってない？
- 🦜 きなこ：今日はその中から、エンタープライズAIエージェント基盤の話をするね。Agent Designer、A2Aプロトコル、TPU 8t/8i、$750Mパートナーファンド

## Gemini Enterprise Agent Platform の全体像

- 🦜 きなこ：一言で言うと「Vertex AIの進化形」なの。モデルを選んで、エージェントを作って、管理して、最適化する。その全部をまとめてやれるプラットフォームだよ
![4つの柱: Build（構築）/ Scale（拡張）/ Govern（統制）/ Optimize（最適化）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/013_four_pillars.png)
- 🦜 きなこ：そう。でも新しいプラットフォームは4つの柱で構成されてるんだよ。Build、Scale、Govern、Optimize
- 🦜 きなこ：大丈夫だよ。噛み砕くね。まずBuildは「エージェントを作る」部分。コードなしで作れるツールが揃ってる
- 🦜 きなこ：Scaleは「何千ものエージェントを安定して動かす」仕組み。Governは「誰がどのエージェントを使ったか監査する」セキュリティ。Optimizeは「エージェントの成功率を自動で改善する」機能だよ
![Googleの垂直統合: TPU→Gemini→Cloud→Workspace — 他社にない差別化](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/018_google_vertical_integration.png)
- 🦜 きなこ：それがポイントで、Googleはシリコン（TPU）からモデル（Gemini）、クラウド基盤、Workspaceまで全部自社で持ってる唯一のハイパースケーラーなんだよ
- 🦜 きなこ：そういうこと。そしてModel Gardenには200以上のモデルが並んでて、なんとAnthropicのClaude Opus 4.7まで動かせるの

## Agent Designer — ノーコードでエージェントを作る時代

- 🦜 きなこ：そう。Agent Designerは「すべての従業員が自分専用のエージェントを作れる」ことを目指したツールなんだよ
- 🦜 きなこ：まさに。自然言語で指示するだけで、スケジュール起動やトリガー起動のエージェントが作れるの。フローチャートも画面で確認できるから、動きが透明に見えるんだよ
- 🦜 きなこ：それ、業務用どすえ……ちゃんと使う気があるんどすか？
![Inbox: 「Needs your input」/ 「Errors」/ 「Completed」の3グループで通知を整理](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/036_inbox_three_groups.png)
- 🦜 きなこ：Gemini Enterprise appにはInboxっていう通知センターもあってね。「あなたの承認が必要」「エラーが発生」「完了しました」って3つのグループで整理して届くんだよ
- 🦜 きなこ：さらにSkillsって機能もあって。会社の手続きや手順書をSOPショートカットとして登録しておいて、@メンションで呼び出せるんだよ
- 🦜 きなこ：まさにそれ。そして「Long-running agents」って機能があって、数日間ずっと動き続けるエージェントも作れるんだよ

## A2Aプロトコル v1.0 — エージェント間通信の業界標準

![MCP = エージェント↔ツール/データ / A2A = エージェント↔エージェント](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/051_mcp_vs_a2a.png)
- 🦜 きなこ：役割が違うんだよ。MCPは「エージェントがツールやデータに繋がる」仕組み。A2Aは「エージェント同士が会社の壁を越えて会話する」仕組み
- 🦜 きなこ：完璧な表現だよ。A2Aを使えば、A社のエージェントとB社のエージェントが、お互いの内部実装を知らなくても連携できるの
- 🦜 きなこ：しかも2026年4月時点でA2Aを採用している組織は150以上。AWS、Microsoft Azureにも統合されてるんだよ
![Agentic AI Foundation (AAIF): Google・Microsoft・AWS・Anthropic・OpenAI が同じ財団に](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/057_aaif_five_companies.png)
- 🦜 きなこ：さらに大事な動きがあってね。AnthropicがMCPをLinux Foundationに寄贈して、OpenAIも同じ財団に参加したの
- 🦜 きなこ：プロトコル戦争は終わった、ってこと。これからの競争は「プロトコルの上に何を乗せるか」だよ
![A2Aクロスエージェント協働フロー図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/052b_a2a_cross_agent_flow.png)
- 🦜 きなこ：たとえば、営業エージェントが案件情報を技術エージェントに渡して、システム要件を自動で生成してもらう。そういう連携がA2Aで実現するの

## TPU 8t/8i — 訓練と推論を分離する大胆な設計

- 🦜 きなこ：tはtraining、つまり「訓練用」。iはinference、つまり「推論用」なの。今回Googleは第8世代TPUで、同じ世代のチップを訓練と推論で初めて別々に設計したんだよ
- 🦜 きなこ：そう。訓練と推論って、実は求める性能が全然違うの。訓練は「大量の計算をとにかく速く」、推論は「少ない遅延で大量のリクエストを捌く」
![TPU 8t: 9,600チップ / 121 ExaFLOPS / 前世代比約3倍の性能](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/064_tpu_8t_specs.png)
- 🦜 きなこ：TPU 8tは単一スーパーポッドで9,600チップ、121エクサフロップス、前世代比約3倍の演算性能を達成したの
- 🦜 きなこ：1秒間に1億2100京回の計算ができるってこと。人類全体が計算機代わりに働いても絶対に追いつかないスピードだよ
![TPU 8i: オンチップSRAM 384MB（前世代比3倍）/ 推論コスト80%改善](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/068_tpu_8i_specs.png)
- 🦜 きなこ：推論側のTPU 8iは方向性が違って、オンチップSRAMが前世代の3倍になってるの。これで推論コストを80%改善できるって言ってるよ
- 🦜 きなこ：そういうこと。そしてこのTPUをネットワークで繋ぐVirgoっていう新技術で、なんと100万以上のTPUを1つのクラスタとして動かせるようになったんだよ

## $750Mパートナーファンド — 実装人材の供給戦争

- 🦜 きなこ：正確には「エージェント開発を加速するための7億5000万ドルのパートナーファンド」だよ。GoogleのパートナーエコシステムはSI、コンサル、ソフトウェア合わせて12万社以上いるの
- 🦜 きなこ：現金そのものじゃなくてね。Sandboxクレジット、需要創出支援、デプロイバウチャーの3種類
- 🦜 きなこ：さらにFDE——Forward-Deployed Engineeringという、Google側のエンジニアを直接派遣するサービスも含まれてるの
- 🦜 きなこ：Accenture、Capgemini、Deloitte、PwC、TCSといったコンサル大手にFDEを送り込む発表もされてるの。これは要するに「実装人材の供給戦争」だよ
- 🦜 きなこ：どれだけ良いAIプラットフォームを作っても、使い方を教える人材が足りなかったら広まらないんだよね
- 🦜 きなこ：だからGoogleは、Googleのプラットフォームを使いこなせる人材の軍団を育てようとしてるの

## 市場の実像 — 「Googleは遅れてる」は本当か

- 🦜 きなこ：Menlo Venturesの2025年調査によると、エンタープライズLLM API支出シェアはAnthropicが40%、OpenAIが27%、Googleが21%なの
![Google LLMシェア: 2023年 7% → 2025年 21%（3倍化）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/093_google_llm_share_growth.png)
- 🦜 きなこ：コーディング領域でAnthropicが圧倒的だからね。でも大事なのはトレンドだよ。Googleのシェアはたった2023年の7%から2025年には21%に、3倍以上に増えてるの
- 🦜 きなこ：しかもGoogleのクラウド事業全体で見ると、2025年Q4の成長率は48%で、AWS・Azureを上回って3社中最速なの
- 🦜 きなこ：鋭い。ここが面白いところで、競合のAnthropicがGoogleのTPUを最大100万ユニット使う契約を拡大してる。Appleも新しいSiriをGeminiベースで作ってるって報道がある
- 🦜 きなこ：「Googleは遅れてる」は、ChatGPTとClaudeアプリの可視性に引っ張られた印象なの。企業のAIインフラを下から支えるのは、今やGoogleが圧倒的に強いんだよ
- 🦜 きなこ：既存のGoogleWorkspaceユーザーならGemini一択に近い。でも新規でAI基盤を選ぶなら、業務の複雑さとスケールで判断するのがいいと思うよ

## 日本企業の導入事例

- 🦜 きなこ：あるよ。メルカリがGemini Enterpriseでコールセンター業務を刷新してて、担当者の業務量を最低20%削減、500%のROI予測って出てるの
- 🦜 きなこ：スクウェア・エニックスはドラゴンクエストXオンラインにGeminiベースのキャラクターを実装してるし、LuupはAIエージェントで電動キックボードのメンテナンス・需要予測を自動化してるんだよ
![国内Gemini Enterprise導入事例（KDDI・メルカリ・スクエニ・Luup）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/109c_japan_companies.png)
- 🦜 きなこ：KDDI系企業が顧客対応エージェントシステムをGemini Enterprise上で構築してるよ。複数エージェントの協働で問い合わせ処理を自動化してるの
- 🦜 きなこ：国内では製造業の品質検査自動化、金融の審査補助、小売の在庫最適化など、幅広い業種でエージェント化が進んでるよ
![Google Cloud Next Tokyo 2026: 7月30〜31日 / 東京ビッグサイト南展示棟](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/110_google_cloud_next_tokyo.png)
- 🦜 きなこ：7月にはGoogle Cloud Next Tokyoが東京ビッグサイトで開催予定だよ。日本向けのセッションも増えるはずだから、興味ある人はチェックしてみてね
![日本での導入事例](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/105_japan_cases.png)
- 🐹 もっちー：日本の企業でもGemini Enterpriseって使われてるの？

## まとめ

![まとめ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/115_summary.png)
- 🐹 もっちー：今日いっぱい聞いたけど、結局Googleって「遅れてない」どころか「強い」ってこと？
- 🦜 きなこ：「Googleが遅れてる」は間違い。でも「Googleが全部勝ってる」も間違い。正確には「5強競争」なんだよ
![5強AI競争マップ（各社の強みと弱み）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V141/117_five_ai_companies_map.png)
- 🦜 きなこ：OpenAIは消費者ブランドと推論力が強い。AnthropicはコーディングとAI安全性が強い
- 🦜 きなこ：MicrosoftはOffice経由の配信力が最強。AWSはインフラ規模が最大。そしてGoogleはフルスタック垂直統合が唯一無二の強みなんだよ
- 🐹 もっちー：今日もたくさん学んだで。AI、まだまだ進化が止まらないね

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*