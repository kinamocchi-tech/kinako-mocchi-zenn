---
title: NVIDIAなしでAIを作った？中国Z.aiとGLM-5.1を解説【解説記事】
emoji: 🤖
type: tech
topics:
- swe-bench
- ai
- llm
- tech
published: true
---

# NVIDIAなしでAIを作った？中国Z.aiとGLM-5.1を解説

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [NVIDIAなしでAIを作った？中国Z.aiとGLM-5.1を解説](https://www.youtube.com/watch?v=bPj454ZQCFI)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、AI作るのってNVIDIAのGPUがないと無理なんでしょ？
- 🐹 もっちー：えっ、ひっくり返ったって？だって全世界のAI企業がNVIDIA争奪戦してるんだよね
![GLM-5.1のロゴと754B MoEパラメータ表示、リリース日2026年4月7日](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/004_glm51_launch.png)
- 🦜 きなこ：今日のテーマはGLM-5.1。中国のZ.aiが4月7日に公開した754B MoEモデルよ
- 🐹 もっちー：NVIDIAなしで！？ワシ、それ信じられへん。なんでそんなことできるん？

## GLM-5.1リリースと衝撃の事実

![Z.ai企業情報: 清華大学発、2019年6月設立、世界初の上場済みLLM企業](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/013_zai_company_info.png)
- 🦜 きなこ：まず、GLM-5.1を作ったZ.aiという会社を紹介するね
- 🦜 きなこ：中国の清華大学から2019年に独立したAIスタートアップで、創業者は清華大学教授の唐杰氏よ
![GLM-5.1の基本仕様テーブル: 754B総パラメータ・40Bアクティブ・256エキスパート中Top-8ルーティング・200Kコンテキスト](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/016_glm51_specs.png)
- 🦜 きなこ：まず規模がすごいの。総パラメータ数は約754Bで、200Kトークンまで扱えるの
![MoE構成のイメージ図: 巨大な本棚(754B)から関連する少数の本(40B)だけを取り出して使うメタファー](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/018_moe_diagram.png)
- 🦜 きなこ：じゃあ例えるね。図書館に7540億冊の本が並んでるの。でも質問に答えるときは、関係ある400億冊だけを読むイメージ
- 🦜 きなこ：そう、この仕組みをMoE、つまり混合エキスパートっていうの。今のフロンティアモデルはほとんどこの方式よ
![SWE-Bench Pro概要: 41リポジトリ・1,865タスク・平均107行・4.1ファイルの変更要求](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/022_swe_bench_overview.png)
- 🦜 きなこ：Scale AIの業界最難関コーディングテストよ

## なぜHuaweiチップだけで可能だったのか

![章タイトル: なぜHuaweiチップだけでフロンティアモデルが作れたのか?](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/034_chapter_huawei.png)
- 🦜 きなこ：ここからが本題。なぜGLM-5.1がHuaweiチップだけで作れたのか、解き明かしていくね
![Huawei Ascend 910Bチップ画像・スペック表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/035_ascend_910b.png)
- 🦜 きなこ：使われたチップはHuawei Ascend 910B。米国のGPU輸出規制を受けて、中国が国産化を進めた切り札よ
![性能比較テーブル: Ascend 910Bは H100比でFP16性能32-40%、メモリ帯域36-48%、チップ間通信44%](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/037_performance_comparison.png)
- 🦜 きなこ：CSETの分析だと、Ascend 910Bの演算性能はH100の約32から40%。メモリ帯域は36から48%にとどまるの
![スケール戦略イメージ: 10万基クラスターの可視化](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/039_scale_strategy.png)
- 🦜 きなこ：答えは2つ。1つ目はスケールで補うこと。Z.aiはAscend 910Bを約10万基使ったの
- 🦜 きなこ：1基ずつは性能劣るけど、数で押し切る戦略。人海戦術ならぬチップ海戦術ね
![非同期RLインフラ「slime」の概念図: 生成と評価を並列化](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/042_slime_infrastructure.png)
- 🦜 きなこ：2つ目がソフトウェアの工夫。Z.aiが独自開発した非同期強化学習フレームワーク「slime」が鍵なの

## 「世界首位」の真実

![章タイトル: スキャフォールディング問題とは](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/059_chapter_scaffolding.png)
- 🦜 きなこ：「世界首位」の主張にはスキャフォールディング問題があるの
![スキャフォールディング概念図: 同じAIでも足場(ツール)によって成績が変わる](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/061_scaffolding_concept.png)
- 🦜 きなこ：スキャフォールディングは足場の意味。AIに問題を解かせるときに、どんな道具を使わせるかの設定のことよ
- 🦜 きなこ：例えば、もっちーに算数テストを受けさせるとき、電卓ありと電卓なしで点数が違うでしょ？
- 🦜 きなこ：AIも同じで、ツールの使い方次第でスコアが10ポイント以上変わるの
- 🦜 きなこ：で、ここが問題。Z.aiは自分たちで作ったOpenHandsという足場を使って測定したの
![Scale AI SEAL標準化リーダーボード概念図: 全モデル同一条件・250ターン制限・mini-swe-agentハーネス](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/067_seal_concept.png)
- 🦜 きなこ：そこまでは言えないけど、Scale AIが公式にやってる標準化リーダーボード、SEALには未登録なの

## 米中半導体戦争の新局面

![章タイトル: 米中半導体戦争の新局面](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/083_chapter_semiconductor_war.png)
- 🦜 きなこ：ここから話を広げるね。GLM-5.1が示したのは、単なる技術的快挙じゃないの
- 🦜 きなこ：米国が仕掛けた半導体制裁の「常識」を、根底から揺さぶる出来事なの
![2022年10月7日規則のタイムライン](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/086_october_2022_timeline.png)
- 🦜 きなこ：2022年10月、バイデン政権が先端AIチップの対中輸出を禁止したの。約30年の半導体政策を転換した瞬間よ
- 🦜 きなこ：目的は、中国のAI軍事利用を牽制することと、米国のAI技術優位を守ること
![制裁効果2大論争の対比図: 機能している派(CFR,FDD) vs 逆効果派(CEPA,Contrary Research)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/089_sanctions_debate.png)
- 🦜 きなこ：実はここで意見が真っ二つに分かれてるの。「制裁は機能している派」と「制裁は逆効果派」
![CFR分析: 米中チップ性能格差 現在5倍・2027年予測17倍](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/090_us_china_chip_gap.png)
- 🦜 きなこ：機能してる派の根拠はCFRの分析。米国最先端チップは中国最良品の約5倍で、2027年に17倍に広がると予測してるの

## 私たちエンジニアに何が起こるのか

![章タイトル: 私たちエンジニアに何が起こるのか](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/109_chapter_engineers.png)
- 🦜 きなこ：最後にね、この変化が私たちエンジニアや開発者に何をもたらすのか、考えてみたいの
![エンジニアへの影響3つ: ①激安AIツール ②自律エンジニアの登場 ③AI選択肢の多様化](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/111_three_impacts.png)
- 🦜 きなこ：大いに関係あるの。まず1つ目、高性能AIコーディングツールが激安で使えるようになる
- 🦜 きなこ：中国モデルは米国の6分の1から4分の1の価格。Claude OpusやGPT-5と同等性能でも、年間だと大きな差になるの
- 🦜 きなこ：2つ目、自律エンジニアの現実化。GLM-5.1の8時間自律タスクは、バイブコーディングを超える世界を示唆してるの
![ヴァイブコーディングの定義: AIとの対話ベースの開発スタイル(Andrej Karpathy提唱)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/116_vibe_coding.png)
- 🦜 きなこ：AIと対話しながら感じで書く開発スタイルのこと。Andrej Karpathyさんが広めた言葉よ
- 🦜 きなこ：でもGLM-5.1が目指しているのは、その先。人間が寝ている間にAIが8時間自律的にエンジニアリングする世界

## まとめ

![まとめスライド: 今日の3つのポイント](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/133_summary_slide.png)
- 🦜 きなこ：じゃあ、今日のまとめね
![ポイント1: NVIDIA不要でのフロンティアモデル実現](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/134_point1_nvidia_free.png)
- 🦜 きなこ：1つ目、GLM-5.1は中国Z.aiがHuawei製だけで作った754B MoE。NVIDIAなしで最前線を実現したの
![ポイント2: 世界首位主張は条件付き、ただし世界トップ3の実力は確実](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/135_point2_conditional_claim.png)
- 🦜 きなこ：2つ目、「世界首位」主張は条件付き。SEAL標準化では未検証だけど、コーディング能力は世界トップレベルで確実なの
![ポイント3: 米中半導体戦争の新局面とアルゴリズム革新](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V117/136_point3_semiconductor_war.png)
- 🦜 きなこ：3つ目、米中半導体戦争は新局面へ。ハードウェア格差はあるけど、アルゴリズム革新で中国は追い上げ中なの

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*