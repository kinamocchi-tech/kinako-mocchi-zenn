---
title: 科学者の2年分の仕事が数週間に？Anthropic「Claude Science」の正体とその代償【解説記事】
emoji: 🐹
type: tech
topics:
- ai
- llm
- tech
published: true
---

<!-- グラレコ:graphreco -->
![科学者の2年分の仕事が数週間に？Anthropic「Claude Science」の正体とその代償【解説記事】｜グラレコ要約](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/V239_graphreco.png)

# 科学者の2年分の仕事が数週間に？Anthropic「Claude Science」の正体とその代償

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [科学者の2年分の仕事が数週間に？Anthropic「Claude Science」の正体とその代償](https://www.youtube.com/watch?v=Z96wRZgYSUw)
:::

## この記事で分かること

- 🐹 もっちー：え、科学者が2年かけてた論文レビューが、たった数週間で終わったって！？
- 🐹 もっちー：いつものClaude！？モデル変えてないのに、なんでそんなに速くなるの？
![Claude Science official announcement banner image](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/004.png)
- 🦜 きなこ：今日はAnthropicが発表した研究者向けの仕組み『Claude Science』を深掘りしていくね
![Small preview icon: research grants teaser](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/009.png)
- 🐹 もっちー：太っ腹な助成金の話まで出てくるって聞いたけど、そっちも本当に見逃せない内容だったりする？

## Claude Scienceの正体

![Title card in English: 'Claude Science = NOT a new model'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/016.png)
- 🦜 きなこ：ううん、そこが一番の勘違いポイントなの。中身は今までのClaudeがそのまま動いてるだけで、モデル自体は何も新しくなってないんだよ
![Diagram: existing Claude model at the bottom, a new 'Workbench layer' stacked on top](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/018.png)
- 🦜 きなこ：実はモデル名は公式には書かれてないの。報道ではOpus 4.8とも言われてる。新しいのはそれを動かす「ワークベンチ」の方なんだよ
![Illustration: a workbench with research tools and reference books laid out side by side](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/020.png)
- 🦜 きなこ：その感覚で合ってるよ。研究に必要な道具と資料を一か所に並べて、すぐ手に取れるようにした作業台、ってイメージで大丈夫なんだよ
- 🦜 きなこ：これまでは研究者自身が、データベースごとに違う書式やクエリ言語を何年もかけて覚えて、手作業で行き来してたんだよ
![Hub-and-spoke diagram: one coordinator agent at the center, 60+ skills and scientific databases around it](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/021.png)
- 🦜 きなこ：そこにまとめ役のエージェントが一体いてね。プロジェクトマネージャーみたいな存在で、60を超えるスキルや科学データベースへ代わりに繋ぎに行ってくれるの
![Database list in English: UniProt / PDB / Ensembl / Reactome / ClinVar / ChEMBL / GEO](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/023.png)
- 🦜 きなこ：UniProtやPDB、Ensemblとかね。タンパク質の百科事典に、立体構造の図鑑、遺伝子の地図みたいなものが最初から繋がってるの

## Allen Instituteの実例

![Term card: Actor-Critic pattern, a writer agent icon and a reviewer agent icon facing each other](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/033.png)
- 🦜 きなこ：それ、アクター・クリティック方式っていう組み立て方なんだよ。Claude Scienceの実例でも、ちゃんとその形が使われてるの
![Split diagram: Actor agent drafting a document on the left, Critic agent checking citations on the right](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/035.png)
- 🦜 きなこ：アクターが書く担当で、クリティックが検証担当なの。作文する係と、その作文を赤ペンで採点する係が、最初から別々に用意されてる感じだよ
- 🦜 きなこ：そこが肝心なの。同じエージェントに書かせて、そのまま自分で点検させると、書いたときと同じ思考のまま読むから、自分の間違いになかなか気づけないんだよ
![Callout: self-review blind spot, a single agent inspecting its own draft and missing its own error](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/038.png)
- 🦜 きなこ：これは検証バイアスって呼ばれるものなの。自分の答えは正しいはずっていう思い込みが、点検する目を曇らせちゃうんだよ
- 🦜 きなこ：そういうこと。書く側と検証する側を最初から切り離しておけば、その甘さをかなり減らせるの。手間は倍でも、間違いが減る方を取った設計なんだよ
![Profile card: Jerome Lecoq, neuroscientist at Allen Institute, with a pipeline diagram built from about 20 custom skills](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/042.png)
- 🦜 きなこ：いるんだよ。アレン研究所の神経科学者、ジェローム・ルコックさん。独自スキルを約20個も組み合わせて、自分専用のパイプラインを作ったの

## 太っ腹な助成金プログラム

- 🦜 きなこ：その疑い方、私は正しいと思うよ。ただ中身を見ないと、裏があるかどうかも判断できないでしょ。だからまず、お金の出し方を順番に整理するね
![Two separate grant program cards placed side by side, labeled 1 and 2](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/051.png)
- 🦜 きなこ：大事なのは、この助成がひとつじゃないってこと。名前も金額も締切も違う、性格の異なる助成が2つ走っているの。ここを混ぜると話がややこしくなるんだよ
![Grant 1 card: Claude Science launch grants, up to 50 projects, up to $30,000 in API credits each](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/052.png)
- 🦜 きなこ：ひとつ目がClaude Science立ち上げ助成。最大50件のプロジェクトに、1件あたり最大3万ドル分のクレジットを出すプログラムなの
![Deadline stamp over Grant 1 card: July 15, 2026 - CLOSED](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/054.png)
- 🦜 きなこ：落ち着いて。この立ち上げ助成の応募締切は2026年7月15日で、この動画を撮っている時点ではもう過ぎているの。今から応募はできないんだよ
![Grant 2 card: rare disease research grants, co-run with the Monarch Initiative](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/056.png)
- 🦜 きなこ：そこで諦めないで。もうひとつのほうはまだ動いてるの。Monarch Initiativeという研究チームと組んだ、希少疾患の研究者向けの助成だよ
![Grant 2 details: up to $50,000 in credits over six months, deadline August 2, 2026 11:59 PM PST](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/057.png)
- 🦜 きなこ：こっちは6ヶ月で最大5万ドル分のクレジット。応募締切は2026年8月2日の太平洋時間、夜11時59分で、残り時間はもうほとんどないの

## 実はここまでいいことばかり

![Caption card: Lecoq himself admits the limits of this workflow](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/063.png)
- 🦜 きなこ：実はね、Lecoq氏本人が、このやり方の限界をはっきり認めてるんだよ。いいところしか話してこなかったから、ここからは影の部分も話すね
![Note card: struggles to judge paper quality beyond citation counts](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/069.png)
- 🦜 きなこ：そう。有料の壁の向こうは読めないの。しかも論文の質の評価にも苦戦してて、引用数は数えられても、その研究の中身が良いかまでは測りきれないんだよ
![Warning card: the two-years-to-weeks figure is Anthropic's own self-reported number, with no third-party verification](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/071.png)
- 🦜 きなこ：そこも正直に言うね。あれはAnthropic自身が出した自己申告の値で、第三者が検証したものじゃないの。約10本っていう数もそう
- 🦜 きなこ：信じたくなる数字ほど、誰が測ったのかを見る癖を持ちたいの。それとね、危ないのは数字の出どころだけじゃないの
![Diagram: data stays on the lab machine, but the papers being read can carry hidden instructions](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/075.png)
- 🦜 きなこ：機密データは手元で動かせるから安心って話をしたよね。でも守れるのは持ち出しの方だけで、読み込む論文の側に仕掛けが埋め込まれてることがあるの
![Diagram: white or tiny hidden text in a manuscript instructing the reviewing AI to accept the paper](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/077.png)
- 🦜 きなこ：隠しプロンプトインジェクション。白い文字や極小の文字で、この論文を採択せよって指示を論文に紛れ込ませるの。実験だと成功率98%超の報告もあるよ

## AI for Science三つ巴の構図

![Three-way race in AI for Science: Anthropic / OpenAI / Google DeepMind](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/084.png)
- 🦜 きなこ：ううん、そこは早とちりなんだよ。OpenAIもGoogle DeepMindも同じ場所を狙っていて、AI for Scienceは三つ巴の争いになってるの
- 🦜 きなこ：といっても、三社の機能をきちんと比べた公開データはまだ無いの。だからここは優劣じゃなくて、業界の大きな構図の話として聞いてね。細かい比べっこはこれからの話
- 🦜 きなこ：それがね、いちばんおもしろいところなんだよ。Anthropicはこの競争で、モデルの賢さそのものでは勝負してないの。そこが今回の肝なんだよ
![Not a new model: existing Claude + workflow environment](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/088.png)
- 🦜 きなこ：思い出してほしいの。Claude Scienceは新しいモデルじゃなくて、既存のClaudeを動かすワークフローの環境だったよね
![Point of difference: WHERE the AI runs (design philosophy)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/090.png)
- 🦜 きなこ：そう。だからAnthropicが競ってるのは性能の数字じゃなくて、そのAIをどこで動かすのかっていう設計思想のほうなんだよ
![Runs on the lab's own infrastructure: local macOS/Linux, SSH, HPC login node](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/091.png)
- 🦜 きなこ：Claude Scienceが動くのはラボ自身のインフラの上。macOSやLinuxのローカルでも、SSH越しやHPCのログインノードでも動くの

## まとめ

![Summary chart: identity vs case studies vs concerns comparison table](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/097.png)
- 🦜 きなこ：まとめるとね、Claude Scienceは新モデルじゃなくてワークベンチ。実例そのものは本物だけど、数字は自己申告だったの
- 🦜 きなこ：太っ腹な助成金も、モデル性能じゃなくて研究現場に根づかせるための戦略だったって話、忘れないでほしいな
- 🐹 もっちー：これ保存しとこ！引用ハルシネーションとか隠しプロンプトの話、また忘れちゃいそうだし
![Small channel subscribe reminder icon](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V239/099.png)
- 🦜 きなこ：こういう最新のAI事情、チャンネル登録が増えるともっと早く深掘りして届けられるようになるんだよ

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*