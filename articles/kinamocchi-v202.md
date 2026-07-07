---
title: SNSデマ！「Windows AIエージェントOS」とNVIDIA RTX Sparkの真実【解説記事】
emoji: 🤖
type: tech
topics:
- ai
- kb5039239
- nvidia
- llm
- tech
published: true
---

# SNSデマ！「Windows AIエージェントOS」とNVIDIA RTX Sparkの真実

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [SNSデマ！「Windows AIエージェントOS」とNVIDIA RTX Sparkの真実](https://www.youtube.com/watch?v=-fj9SSQj-sU)
:::

## この記事で分かること

- 🐹 もっちー：え！？嘘やん…SNSであんなに拡散しとったのに、デマやったん？
- 🐹 もっちー：全然別物やん…なんやその、スパーク何ちゃらて。チップなん？ソフトなん？頭こんがらがってきた…
- 🐹 もっちー：ほな今日の動画では、まず本物の RTX Spark の正体と、Foundry on Windows ってやつを順番に見ていく感じ？
![RTX Spark Superchip ティザー画像（スペック数値はぼかし）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/014_rtx_spark_teaser.png)
- 🦜 きなこ：でもね、本物の RTX Spark のスペック、ちょっと普通じゃないんよ。これ見たらデマが霞むレベル。まずはそこから見ていくね

## RTX Spark Superchip の発表とコアスペック

![RTX Spark Superchip の NVIDIA 公式プレス画像を中央に表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/017_rtx_spark_product_card.png)
- 🦜 きなこ：じゃあ、本物の RTX Spark Superchip がどんなチップなのか、公式情報から順番に見ていくね
![発表日「2026-05-31 GTC Taipei」のタイムラインバナーを表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/018_announcement_timeline_banner.png)
- 🦜 きなこ：発表は 2026 年 5 月 31 日、GTC Taipei。Computex 2026 のウィンドウ内に被せた、NVIDIA の本気の打ち上げなんだ
![スペック比較表（GPU/CPU/メモリ/FP4性能の4行レイアウト・空欄状態）を表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/019_spec_table_empty.png)
- 🦜 きなこ：中身は GPU と CPU が NVLink-C2C ってチップ間接続で繋がった、いわゆる「スーパーチップ」構成なの
![スペック表 GPU 行に「Blackwell RTX / 6,144 CUDA / 第5世代Tensor・FP4」を埋める](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/020_spec_table_gpu_filled.png)
- 🦜 きなこ：GPU は Blackwell RTX で 6,144 CUDA コア。第 5 世代 Tensor コアで FP4 精度に対応してるんだよ
![スペック表 CPU 行に「20コア NVIDIA Grace（Arm・MediaTek共同設計）」を埋める](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/021_spec_table_cpu_filled.png)
- 🦜 きなこ：CPU 側は 20 コアの NVIDIA Grace CPU。Arm ベースで、MediaTek と共同設計してるの
- 🦜 きなこ：そこ、よく混同される部分なんだ。CPU はあくまで NVIDIA Grace で、MediaTek 単独設計じゃなくて共同設計なんだよ

## メモリ帯域『300GB/s』の真相 — DGX Sparkとの混同

![RTX Spark スペック表と DGX Spark スペック表を左右並列表示。RTX Spark 側の帯域欄に「未公表」と赤字、DGX Spark 側に「273 GB/s」と表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/029_rtx_vs_dgx_spark_comparison.png)
- 🦜 きなこ：実はね、RTX Spark のメモリ帯域は NVIDIA の公式製品ページにも、プレスリリースにも一切明記されてないんだ
![DGX Spark スペック表側を赤マーカーで強調しズームイン](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/032_dgx_spark_highlighted.png)
- 🦜 きなこ：じゃあなんで「300GB/s」って数字が出回ってるのか。一番ありそうなのが、近接製品との取り違えなんだ
- 🦜 きなこ：RTX Spark の隣に、DGX Spark っていう別製品があるの。中身は GB10 Grace Blackwell Superchip
![DGX Spark 側に「LPDDR5x / 128GB / 256-bit / 273 GB/s」をハイライト表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/034_dgx_spark_memory_specs.png)
- 🦜 きなこ：この DGX Spark のメモリが、LPDDR5x の 128GB・256-bit バス・帯域 273 GB/s ってちゃんと公式に明記されてるんだ
- 🦜 きなこ：そう、その線が濃いの。両方とも Grace CPU + Blackwell GPU の同じシリコンファミリだから、書く側もうっかり混ぜちゃいやすいんだよ
- 🦜 きなこ：ただ大事なのは、DGX Spark は Linux 開発者向けの別プラットフォームで、RTX Spark の Windows コンシューマ機とは別物ってこと

## 出荷計画とOEMパートナー — Surface Laptop Ultraの存在

- 🦜 きなこ：初期パートナーは ASUS、Dell、HP、Lenovo、Microsoft、MSI の 6 社なの
- 🦜 きなこ：あとから Acer と GIGABYTE も続くって公式が明言してるんだよ
![『Surface Ultra』に取り消し線、『Surface Laptop Ultra』に正解マーク](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/045_surface_laptop_ultra_correction.png)
- 🦜 きなこ：そこ、ネットで間違いが多いとこなの。正式名は「Surface Laptop Ultra」なんだよ
- 🦜 きなこ：実は全社未公表なの。アナリスト推定で $1,799 と $2,899 って数字が出回ってるけど、これは MSRP じゃないの
![Surface RTX Spark Dev Box の概念図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/047b_surface_dev_box_concept.png)
- 🦜 きなこ：いい質問なの。実は同じシリコンを Microsoft が『Surface RTX Spark Dev Box』として開発者向けに別途出すと公表してて、開発者は秋を待たずに触れる可能性があるんだよ
![OEM 8社のロゴ集合と『Windows PC ほぼ全員参加』のキャプション](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/047c_oem_all_participate.png)
- 🦜 きなこ：あとね、初期6社+後続2社のラインナップ見るとわかるけど、これ実質 Windows PC 主要OEMほぼ全員参加なの。それくらい NVIDIA と Microsoft が組んだ意味は大きいんだよ

## Microsoft Foundry on Windows と Windows MLの正体

- 🦜 きなこ：正しい名前は「Microsoft Foundry on Windows」なんだよ
- 🦜 きなこ：これは 3 つの技術の総称で、Windows AI APIs、Foundry Local、Windows ML が中身なの
- 🦜 きなこ：中核は Windows ML なの。2025 年 9 月 23 日に GA、つまり正式提供が始まったんだよ
- 🦜 きなこ：中身は ONNX Runtime っていう推論エンジンで、CPU・GPU・NPU をひとまとめに抽象化してくれるの
- 🦜 きなこ：そう。仕組みの肝が「EP」、Execution Provider って部品なの
- 🦜 きなこ：AMD なら Vitis AI、Intel なら OpenVINO、NVIDIA は TensorRT for RTX、Qualcomm は QNN を Windows ML が自動で選ぶの

## KB5039239デマの解剖 — 実体は2024年6月の通常累積更新

![Microsoft Support サイトに検索バーで『KB5039239』と入力するモック](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/063_microsoft_support_search.png)
- 🦜 きなこ：じゃあ、SNSで拡散してた『KB5039239が6月9日配信』って話、Microsoft一次ソースで実物を確認してみるね
![KB5039239 公式ページのスクショ。日付『June 15, 2024』とビルド番号 26100.863 を赤枠強調](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/064_kb5039239_official_page.png)
- 🦜 きなこ：Microsoft Support の公式ページに載ってるKB5039239、配信日は2024年6月15日。OS Build 26100.863の通常累積更新なの
![KB5039239ページ内の Copilot ピン留め記述を黄色マーカーで強調](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/066_kb_copilot_entry_highlighted.png)
- 🦜 きなこ：しかも公式に書かれてるAI関連の変更は、たった一行『Copilotをタスクバーにピン留めしてアプリとして振る舞う』だけ
![出典追跡のフローチャート](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/068_source_trace_flowchart.png)
- 🦜 きなこ：じゃあ『2026年6月9日 Windows Local AI』って情報、どこから湧いてきたのか追ってみたの
![AI生成集約サイトのドメイン名を一覧表示し、赤い『ランクC未満』スタンプ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/069_low_rank_sites_list.png)
- 🦜 きなこ：windowsnews.ai や chatforest.com みたいなAI生成の集約サイトが発信源。Microsoft 一次ソースには痕跡ゼロなの
![Microsoft Support 検索ボックスに『KB』+番号を入れるだけの3秒チュートリアル](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/071_kb_search_tutorial.png)
- 🦜 きなこ：やり方は単純なの。KB番号を見たらまず Microsoft Support のサイトで検索する。これだけで配信日と中身が全部わかるの

## NPU競合シリコンとDGX Sparkとの切り分け

![『Copilot+ PC 要件: NPU 40 TOPS 超』のタイトルカード](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/075_copilot_plus_pc_requirement.png)
- 🦜 きなこ：まず大前提として、Copilot+ PC を名乗るには NPU が40 TOPS超っていう要件があるの
![3社のNPU TOPS バーチャート](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/076_npu_tops_barchart.png)
- 🦜 きなこ：現行勢は3社。AMD Ryzen AI 300 シリーズが約50 TOPS、Intel Core Ultra 200V が約48 TOPS、Snapdragon X Elite が約45 TOPS
![3階層比較表。下: 既存 Copilot+ PC / 中: RTX Spark Windows / 上: DGX Spark Linux](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/078_three_tier_comparison.png)
- 🦜 きなこ：そうなの。既存の Copilot+ PC が下の階層で、RTX Spark はその上のハイエンド枠。さらに DGX Spark がもう一段違う枠にあるの
![DGX Spark スペック表。OS が『Linux』、用途が『開発・研究』と明記](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/080_dgx_spark_linux_specs.png)
- 🦜 きなこ：切り分けはシンプル。DGX Spark は20コアArm + 128GB LPDDR5x + 273 GB/s、Linux で開発者・研究者向け
- 🦜 きなこ：RTX Spark は Windows で、コンシューマーがエージェント体験を使うためのプラットフォーム。同じシリコンファミリだけど別物なの
![用途別の必要性能比較表](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/082c_llm_performance_table.png)
- 🦜 きなこ：1ペタフロップ FP4 が活きるのは13B〜70B クラスのローカル LLM や、リアルタイム生成系の重い用途なんだよ

## まとめ

![まとめスライド: 『RTX Spark 2026秋 / Windows ML 2025-09 GA』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/085_summary_slide.png)
- 🦜 きなこ：じゃあ今日の整理ね。本物の RTX Spark Superchip は2026年秋出荷待ち、ソフト基盤の Windows ML は2025年9月にもうGA済み
![『KB5039239 = 2024-06-15 通常更新』のキー数値スライド](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/086_kb5039239_key_facts.png)
- 🦜 きなこ：そして KB5039239 は2024年6月の通常更新。AI関連は Copilot タスクバーピン留めだけ。デマに踊らされちゃダメなの
![飼い主のタブレット風画面に『楽しみー』のチャット](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/086a_tablet_chat_screen.png)
- 🐹 もっちー：飼い主さんも『AIエージェントOS楽しみー』って言うてたけど、これデマって伝えたほうがええかな…
![もっちーが胸を張って学びを宣言するアップカット](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/087_mocchi_proud_declaration.png)
- 🐹 もっちー：ぼく今日のいちばんの学びはこれや。KB番号見たら必ず Microsoft Support のサイトで日付確認するわ。これでもうダマされへん
![3ルールまとめスライド](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V202/088a_three_rules_summary.png)
- 🐹 もっちー：ぼく今日学んだ三つのルール、繰り返すで。KB番号は公式で日付確認、Spark 二種類は OS で見分け、『agentic AI OS』は記者の表現や

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*