---
title: Meta Llama 4のLMArena疑惑と本当の実力——Scout/Maverick比較【解説記事】
emoji: 🤖
type: tech
topics:
- meta
- llm
- ai
- scout
- maverick
published: true
---

# Meta Llama 4のLMArena疑惑と本当の実力——Scout/Maverick比較

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [Meta Llama 4のLMArena疑惑と本当の実力——Scout/Maverick比較](https://www.youtube.com/watch?v=sCP0ZlnzTDY)
:::

## この記事で分かること

- 🐹 もっちー：なあなあきなこ！MetaがLlama 4出したんやけど、これ無料で使えるんやろ？OpenAIいらんやん！最強やん！
- 🐹 もっちー：えっ、違うの？ウェイトが公開されてたらタダで使えるんちゃうの？
- 🐹 もっちー：疑惑？なんかコワい話になってきたな
- 🦜 きなこ：今日はLlama 4の全部を一気に解説するよ。Scout vs Maverick、商用化の真相。Muse Sparkへの転換

## Llama API登場の衝撃

![タイムライン: 2025年4月の出来事](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/011_タイムライン__2025年4月の出来事.png)
- 🦜 きなこ：もっちー、その勘違いを解くために、まずは時系列を整理するね
![2025/4/5: Llama 4 Scout/Maverick公開](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/012_2025_4_5__Llama_4_Scout_Maverick公開.png)
- 🦜 きなこ：2025年4月5日、土曜日にLlama 4 ScoutとMaverickがオープンウェイト公開されたの
![オープンウェイト = 重みファイル公開](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/014_オープンウェイト___重みファイル公開.png)
- 🦜 きなこ：ほぼ正解。モデルの重みファイルが公開されていて、自分のPCやサーバーで動かせるんだよ
![2025/4/29: LlamaCon 2025開催](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/015_2025_4_29__LlamaCon_2025開催.png)
- 🦜 きなこ：そして同じ月の29日、Metaが初の開発者カンファレンス、LlamaConを開催したの
![Llama API: 限定プレビュー無料](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/016_Llama_API__限定プレビュー無料.png)
- 🦜 きなこ：そこで発表されたのが、Meta直販のLlama APIの限定プレビュー、しかも無料なの
![2026/4現在: Meta直販API未GA・価格表なし](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/019_2026_4現在__Meta直販API未GA・価格表なし.png)
- 🦜 きなこ：2026年4月の今日時点で、Meta直販APIはまだ正式GAしていないし、公式の価格表もないの

## Scout vs Maverick 技術比較

- 🦜 きなこ：そこ大事なところ。Scoutは効率重視の軽量版、Maverickは性能重視のフラッグシップって役割分担なの
![param_count_compare](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/049_param_count_compare.png)
- 🦜 きなこ：まずScoutは総パラメータ1090億。Maverickは4000億。約4倍近い差があるんだよね
- 🦜 きなこ：ふふ、確かにね。でもここで面白いのが、実際に動くときに使われるパラメータの数なの
![active_param_170b](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/053_active_param_170b.png)
- 🦜 きなこ：そう。「活性化パラメータ」っていうんだけど、ScoutもMaverickも実は170億で同じなんだよ
- 🦜 きなこ：ここに「MoE」っていう仕組みのカラクリがあるの。詳しくは次のセクションで話すね
![scout_h100_single](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/057_scout_h100_single.png)
- 🦜 きなこ：Scoutはね、「単一GPU」、それもNvidia H100一枚で動かせるように設計されてるの

## MoEアーキテクチャ解説

![MoE = Mixture of Experts（専門家の混合）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/087_MoE___Mixture_of_Experts_専門家の混合.png)
- 🦜 きなこ：いい質問。それを理解するには、Llama 4が採用してる「MoE」って仕組みの話が必要なの
- 🦜 きなこ：大丈夫、ゆっくり説明するね。Mixture of Expertsの略で、日本語だと「専門家の混合」っていう意味なの
![Dense（密）: 全員が毎回働く](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/090_Dense_密___全員が毎回働く.png)
- 🦜 きなこ：従来のAIモデルは「Dense」って呼ばれてて、質問が来るたびに全パラメータを動かしてたの
![100人全員召集 → 重い・遅い](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/092_100人全員召集___重い・遅い.png)
- 🦜 きなこ：例えるなら、社員100人の会社で、どんな質問が来ても毎回100人全員を会議室に呼ぶ感じ
- 🦜 きなこ：そう、それが Dense モデルの非効率なところ。電気代もメモリも全員分かかっちゃうの
![Sparse（疎）: 必要な専門家だけ働く](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/095_Sparse_疎___必要な専門家だけ働く.png)
- 🦜 きなこ：そこで登場するのがMoE。質問の内容に応じて「専門家だけ」を呼ぶ仕組みなの

## LMArena操作疑惑

- 🦜 きなこ：MoE設計の話のあとに、ちょっと残念なニュースもあるんだよ
![LMArena = AIモデル人間評価ランキング](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/123_LMArena___AIモデル人間評価ランキング.png)
- 🦜 きなこ：LMArenaっていう、AIモデルの人気投票サイトがあってね
![ユーザーがブラインド投票で勝敗を決定](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/125_ユーザーがブラインド投票で勝敗を決定.png)
- 🦜 きなこ：近いね。人間がAIに同じ質問して、どっちの答えが好きか投票するの
![Llama 4 プレビュー: ELO 1417（世界トップ圏）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/127_Llama_4_プレビュー__ELO_1417_世界トップ圏.png)
- 🦜 きなこ：Llama 4はね、最初プレビュー版でELO 1417を取ったんだよ
- 🦜 きなこ：世界トップ圏。GPT-4やClaudeと並ぶレベルなんだよ
![API公開後: 32位まで急落](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/131_API公開後__32位まで急落.png)
- 🦜 きなこ：でもね、API公開後に同じLlama 4が32位まで落ちたの

## Cerebras爆速と商用エコシステム

![Cerebras Llama 4 Scout: 2,600 tokens/秒](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/157_Cerebras_Llama_4_Scout__2_600_tokens_秒.png)
- 🦜 きなこ：Cerebras経由のLlama 4 Scoutは、毎秒2,600トークン出るんだよ
![一般的なAPI: 60〜100 tokens/秒](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/159_一般的なAPI__60_100_tokens_秒.png)
- 🦜 きなこ：普通のAPIは毎秒60〜100トークンくらいなんだよ
![人間の読速の100倍以上](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/161_人間の読速の100倍以上.png)
- 🦜 きなこ：人間の読む速さの100倍以上なの。読む前に終わるレベルだよ
![Cerebras / Groq: 推論専用チップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/165_Cerebras___Groq__推論専用チップ.png)
- 🦜 きなこ：CerebrasやGroqは、推論専用のチップを使ってるんだよ
![WSE: Wafer Scale Engine](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/167_WSE__Wafer_Scale_Engine.png)
- 🦜 きなこ：そう。CerebrasはWSEっていうウェハー丸ごと一枚のチップなの
- 🦜 きなこ：大丈夫、要はLLM専用に作った超ハイスペック部品ってことだよ

## オープンウェイトの真実

![open_weight_vs_open_source](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/192_open_weight_vs_open_source.png)
- 🦜 きなこ：そこ、みんながよく誤解するところなの。正確には「オープンウェイト」で「オープンソース」じゃないんだよね
![analogy_blueprint_vs_product](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/194_analogy_blueprint_vs_product.png)
- 🦜 きなこ：オープンソースは設計図も製造工程も全部公開する感じ。オープンウェイトは完成品だけ渡す感じ
- 🦜 きなこ：そう！モデルの重みパラメータは公開するけど、学習データとか学習コードとかは非公開なの
![llama_community_license](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/198_llama_community_license.png)
- 🦜 きなこ：Llamaには独自ライセンスがあって、3つの制限があるの
![license_restriction_1_mau](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/200_license_restriction_1_mau.png)
- 🦜 きなこ：まず1つ目。月間アクティブユーザーが7億人を超えるサービスは商用利用に追加ライセンスが必要
![license_restriction_2_no_training](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/202_license_restriction_2_no_training.png)
- 🦜 きなこ：そういうこと。大企業牽制のためのルール。2つ目は、Llamaを使って別のAIモデルを学習させることの禁止

## Muse Spark — Metaのプロプライエタリ転換

![Muse Spark — Meta開発中の新モデル](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/227_Muse_Spark___Meta開発中の新モデル.png)
- 🦜 きなこ：Metaが「Muse Spark」っていう新しいモデルを作り始めたの
![Muse Spark = 完全クローズドモデル](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/229_Muse_Spark___完全クローズドモデル.png)
- 🦜 きなこ：問題はその中身。これ、完全な非公開モデルなの
![戦略転換: オープン → ハイブリッド](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/231_戦略転換__オープン___ハイブリッド.png)
- 🦜 きなこ：そう、ここがまさに戦略転換ポイントなんだよ
![Llama 4 Maverick / Scout = オープンウェイト](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/233_Llama_4_Maverick___Scout___オープンウェイト.png)
- 🦜 きなこ：Llama 4のMaverickとScoutはオープンウェイトで配ってるよね
![最強モデル = 非公開](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/235_最強モデル___非公開.png)
- 🦜 きなこ：でも一番強いMuse Sparkは、外には一切出さないの
![Muse Spark: Meta AIアプリ内のみ / API提供なし](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V131/237_Muse_Spark__Meta_AIアプリ内のみ___API提供なし.png)
- 🦜 きなこ：Meta AIアプリの中だけで動くの。APIすら提供しないの

## まとめ

- 🐹 もっちー：ふう……今日はいっぱい頭使ったな。Llama 4ってほんとに一筋縄でいかない話だった
- 🦜 きなこ：Scout vs Maverick、LMArena疑惑、Muse Spark転換。全部つながってる
- 🐹 もっちー：で、結局もっちーはどうしたらいいの？OpenAIやめてLlama使う？
- 🦜 きなこ：「どっちを使うか」じゃなくて「何に使うか」で選ぶ時代なの。コスト重視ならLlama。品質ならClaude、速度はCerebras

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*