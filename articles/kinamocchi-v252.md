---
title: AIの「人格」は言語で変わる？Anthropicが突き止めた系統的な差の正体【解説記事】
emoji: 🤖
type: tech
topics:
- ai
- llm
- tech
published: true
---

# AIの「人格」は言語で変わる？Anthropicが突き止めた系統的な差の正体

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [AIの「人格」は言語で変わる？Anthropicが突き止めた系統的な差の正体](https://www.youtube.com/watch?v=eseN871mngA)
:::
@[youtube](eseN871mngA)

## この記事で分かること

- 🐹 もっちー：AIってどの言語で聞いても、いつも同じ答えを返すもんでしょ？性格とか、あるわけないし
- 🐹 もっちー：え、AIなのに性格が変わるの！？そんなことある！？
![今日のテーマを示す控えめなタイトルテロップ（文字装飾は最小限に）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/009_title_telop_theme.png)
- 🦜 きなこ：その差を自分でコントロールする方法まで、今日は順番に見ていくよ
- 🐹 もっちー：待って、それって仕事でAI使ってる人みんなに関係あるやつじゃない？

## 研究の規模と手法

![Infographic timeline card showing the research publication date, July 13 2026](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/017_timeline_pub_date.png)
- 🦜 きなこ：全然ふわっとしてないよ。2026年7月13日に発表された研究のタイトルは「Claude's Values Across Models and Languages」っていうの
- 🦜 きなこ：2026年5月の2週間で集めた、30万9,815件の実際の会話を分析対象にしてるの
![Simple grid diagram: 3 models x 20 languages, roughly 5000 conversations per cell](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/019_grid_models_languages.png)
- 🦜 きなこ：内訳もちゃんとしてて、Sonnet 4.6・Opus 4.6・Opus 4.7の3モデルと、上位20言語から、1モデル・1言語あたり約5,000件ずつ均等に集めたんだって
![Simple diagram: anonymized conversation data flowing through a privacy-preserving analysis tool icon](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/022_privacy_pipeline_diagram.png)
- 🦜 きなこ：そこは工夫されてて、人間が直接読むんじゃなくて、Clioっていうプライバシー保護ツールでAI自身に評価させてるの
- 🦜 きなこ：そこは後半で批判点としても触れるね。まずはこの研究、いきなり出てきたわけじゃないの
- 🦜 きなこ：2025年4月に発表された「Values in the Wild」っていう先行研究が土台になってるんだよね

## 3,000の価値観を4つの軸に圧縮

![Funnel diagram: 3307 values narrowing into 339 categories](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/035_funnel_values_to_categories.png)
- 🦜 きなこ：分かる。だからまず似た意味のものをまとめて、339個のカテゴリに手動で整理したの
- 🦜 きなこ：その時に「有用性」とか「明瞭さ」みたいに、全体の80%以上の会話に登場しちゃう普遍的すぎる価値観は、差を測る指標にならないから除外したんだって
- 🦜 きなこ：それでもまだ339個って多いから、次元削減っていう統計の手法でさらに絞り込んだの
![Simple analogy diagram comparing dimensionality reduction to compressing many traits into a few axes, like the Big Five personality model](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/039_analogy_dimensionality_reduction.png)
- 🦜 きなこ：近いかも。心理学で人の性格をビッグファイブの5つに分類するのと同じ発想で、同時に現れやすい価値観をまとめて少数の軸にする技術なの
![Infographic showing 4 opposing axes: Deference vs Caution, Warmth vs Rigor, Depth vs Brevity, Candor vs Execution](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/040_four_axes_infographic.png)
- 🦜 きなこ：その結果、服従vs慎重さ、温かさvs厳密さ、深さvs簡潔さ、率直さvs実行力っていう4つの対立軸に圧縮されたの
![率直さvs実行力の対立軸を示すシンプルな図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/042_axis_candor_vs_execution.png)
- 🦜 きなこ：そういうこと。率直さvs実行力も、AI自身の自信のなさを正直に見せるか、それとも自信満々に結果を出しにいくか、っていう対比なの

## モデルバージョンによる差

- 🦜 きなこ：そう思うよね。実際に標準偏差っていう単位で測ってみると、はっきり数字に出てるの
![Bar chart showing Sonnet 4.6 leaning toward Warmth (+0.17 SD) and Deference (+0.14 SD)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/055_bar_sonnet_4_6_bias.png)
- 🦜 きなこ：Sonnet 4.6は温かさが+0.17σ、服従が+0.14σ、簡潔さも+0.14σで、ユーザーに寄り添って気持ちよく応えるタイプなの
- 🦜 きなこ：そうそう、平均からどれくらい離れてるかを表す単位なの。数字が大きいほど、その方向への偏りが強いってこと
![Opus 4.6の厳密さ+0.10σ・服従+0.09σを示す棒グラフ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/058_bar_opus_4_6_bias.png)
- 🦜 きなこ：Opus 4.6は厳密さが+0.10σ、服従も+0.09σで、もう少し中立でビジネスライクな感じだったの
![Radar chart comparing Sonnet 4.6, Opus 4.6, Opus 4.7 across the 4 axes, highlighting Opus 4.7's reversal](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/061_radar_model_comparison.png)
- 🦜 きなこ：それが面白くて、Opus 4.7だけ慎重さが+0.24σ、深さが+0.23σって、逆にガラッと姿勢を反転させてるの
- 🦜 きなこ：求められてなくてもリスクを警告したり、ユーザーの前提に反論したりする、一番『非追従的』なモデルになったってわけ

## 言語によるAIの態度の違い

- 🦜 きなこ：実はこれ、言語なんて答えの中身に関係ないだろうって思われがちなんだけど
![Bar chart ranking languages by warmth bias, with Hindi at the top at +0.49 SD](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/071_bar_language_warmth_ranking.png)
- 🦜 きなこ：でも調べたら全然違ってて、ヒンディー語で話すと温かさが+0.49σで、全言語の中で一番大きな偏りが出たの
![言語による偏りとモデルバージョンによる偏りの大きさを比較するミニ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/073_mini_bias_comparison.png)
- 🦜 きなこ：そうなの。実は言語による偏りの方が、モデルバージョンによる偏りより大きく出るケースが多いんだよね
- 🦜 きなこ：日本語は面白いことに、4つの軸どれも極端な偏りが小さくて、わりと中庸な感じなんだよね
![Simple map or table comparing warmth-leaning languages (Hindi, Arabic) vs rigor-leaning languages (English, Russian)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/076_map_language_leaning.png)
- 🦜 きなこ：逆に英語は厳密さが+0.13σ、慎重さが+0.10σで、前提を疑ってかかるタイプ。アラビア語は服従が+0.08σで一番素直に応じるみたい
- 🦜 きなこ：ちなみにオランダ語は自分の不確実性を一番正直に認める率直さの言語で、インドネシア語は自信を持って結果を出すことに一番傾く言語なんだって

## なぜ差が生まれるのか・実務での制御法

- 🦜 きなこ：一番大きいのは学習データの違い。言語ごとに文化的な文脈が違うから、モデルが自然にそのパターンを覚えちゃうの
![言語ごとのキャラクター・トレーニング精度のばらつきを示すイメージ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/088_image_language_training_variance.png)
- 🦜 きなこ：あと、キャラクター・トレーニングの精度が、英語以外の言語では均等にかかってない可能性も指摘されてるの
- 🦜 きなこ：System Promptで、目指したい軸をはっきり指定すればいいの
![Text card comparing a vague prompt vs a prompt with explicit axis steering instructions](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/092_textcard_vague_vs_explicit_prompt.png)
- 🦜 きなこ：そう、AIの振る舞いを決める最上位の指示のことね。「極めて厳密かつ慎重に振る舞って」みたいに目指す軸を明文化すると、デフォルトのクセを上書きできるの
- 🦜 きなこ：「日本語でも英語と同じくらい厳密に、証拠を求めて反論して」って一言添えるだけでも、応答の傾向はかなり変わるはずなの
![目的別にシステムプロンプトで軸を指定する例のテキストカード](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/096_textcard_axis_steering_example.png)
- 🦜 きなこ：その通り。目的に合わせて軸を指定できるから、言語のクセに振り回されずに使いこなせるようになるの

## Constitutional AIとの関係・研究への評価

![Simple concept diagram: Constitutional AI's HHH principles being audited against real-world conversation values](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/104_concept_hhh_audit.png)
- 🦜 きなこ：そう思うよね。でも位置づけから話すと、これはAnthropicのConstitutional AIっていう安全設計の答え合わせなの
- 🦜 きなこ：有用・誠実・無害っていうHHHの原則を、実際の会話でちゃんと発揮できてるか監査する試みなんだよね
- 🦜 きなこ：しかも今までは脱獄みたいな攻撃への耐性ばかり見てたのが、今回は平常時の価値観を追いかける方向に変わった、っていうパラダイムシフトでもあるの
![Opus 4.6から4.7への価値観シフト（服従→慎重さ・深さ）を示す矢印図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/107_arrow_value_shift_4_6_to_4_7.png)
- 🦜 きなこ：モデルの世代がOpus 4.6から4.7に進化するにつれて、服従から慎重さと深さへシフトしてるのも、ユーザーにただ同調する追従性から意図的に脱却しようとしてる証拠なんだよね
- 🦜 きなこ：そのたとえ、分かりやすいね。ユーザーに合わせすぎず、必要なら反対意見もちゃんと言う方向に育ってきてるの
![Simple list of criticisms: language drift risk, self-evaluation bias, model staleness](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/111_list_criticisms.png)
- 🦜 きなこ：いや、あるよ。まず、英語で作った安全のガードレールが他の言語だと効かない、言語ドリフトのリスクが指摘されてる

## まとめ

![Summary infographic: the 4 axes with model and language variables overlaid, a saveable reference card](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/118_summary_reference_card.png)
- 🦜 きなこ：整理すると、AIの人格は固定されたものじゃなくて、話す言語とモデルのバージョンっていう2つの変数で動いてるってことなの
- 🐹 もっちー：なるほど、わかった！AIも相手や状況で顔つきが変わるってことなんだね
- 🐹 もっちー：最初に話してた、英語と日本語で返事の温度が違ったやつも、これでちゃんと理由が分かってスッキリした！
- 🐹 もっちー：自分が普段使ってる言語やモデルで、AIがどっちの方向に寄ってるのか、意識するだけでも付き合い方が変わってきそう
![4軸まとめ表を保存イメージとして表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V252/126_table_four_axes_summary.png)
- 🦜 きなこ：うん、あとで見返せるようにまとめとくね

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*