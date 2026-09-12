---
title: Claudeに『見えない透かし』義務化——でも簡単に消せるらしい【解説記事】
emoji: 🤖
type: tech
topics:
- synthid
- c2pa
- ai
- llm
- tech
published: true
---

# Claudeに『見えない透かし』義務化——でも簡単に消せるらしい

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [Claudeに『見えない透かし』義務化——でも簡単に消せるらしい](https://www.youtube.com/watch?v=gMtwBeicKck)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、AIが書いた文章って、コピペしたらもう誰にも分からなくない？
- 🐹 もっちー：え、なにそれ！見た目、全然変わってなくない？
![Abstract close-up: a faint glowing pattern subtly woven between lines of plain text, minimal and mysterious](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/005_visual.png)
- 🐹 もっちー：見えない印！？ほな、AIが書いた文章かどうか、その印を見ればバレるってこと！？
- 🐹 もっちー：厄介？印さえ入れとけば、もう完璧なんちゃうん？

## Claudeに刻まれた『見えない印』の正体

![Diagram: a block of ordinary-looking text with a faint hidden signal pattern woven between the words, revealed under a magnifying glass](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/012_visual.png)
- 🦜 きなこ：そこ、みんなが一番勘違いしやすいところなんだよ。順番に話すから、まず印の正体から一緒に見ていこうね
![Timeline card: Anthropic starts embedding an imperceptible text watermark in Claude models launched on or after August 2, 2026](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/013_visual.png)
- 🦜 きなこ：Anthropicは2026年8月2日以降にリリースするClaudeのモデルから、生成した文章そのものに印を織り込むようにしたの
![Side-by-side illustration: left shows a sticker label pasted onto a document, right shows the signal hidden inside the word choices themselves](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/015_visual.png)
- 🦜 きなこ：イメージは近いよ。でも後からラベルを貼るんじゃなくて、どの言葉をどう並べるかっていう選び方の中に、合図が仕込まれてるの
- 🦜 きなこ：だから私たちの目には何も見えないし、読んでも普通の文章のまま。でも専用のツールで読むと、その合図が拾えるようになってるんだよ
![Product lineup icons in one row: Claude app, Claude Platform API, Claude Code, Claude Cowork, Claude Tag, each stamped with the same hidden watermark badge](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/018_visual.png)
- 🦜 きなこ：ううん、APIもClaude Codeも、Anthropicの主要なプロダクトが対象なの。8月2日以降の対応モデルで作った文章なら全部だよ
![Flow illustration: a sentence copied from a chat window and pasted into a document editor, with the hidden mark traveling along with it](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/020_visual.png)
- 🦜 きなこ：そう、コピーして貼り付けても印は文章にくっついて残るように作られてるの。ちょっと言い回しを直したくらいなら残ることもあるよ

## なぜ今なのか——EUが突きつけた罰則

- 🦜 きなこ：そこなんだよね。実はこれ、Anthropicが善意で思いついて始めた機能、っていうわけでもないの。外から期限を切られてる話なんだよ
![a formal title card showing the EU flag beside a legal article marker. Text on the card in English: 'EU AI Act', 'Article 50 - Transparency obligations', 'applies from 2 August 2026'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/026_visual.png)
- 🦜 きなこ：EU AI Actっていう、EUがAIのために作った規制法があってね。その中の第50条、透明性の義務が、2026年8月2日から適用されはじめたの
![diagram of a text file, an image file and an audio file each receiving a small tag, with a scanner icon reading the tags back afterwards. Labels in English: 'machine-readable mark', 'enable its detection'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/028_visual.png)
- 🦜 きなこ：そう。AIが作った文章や画像や音声には、機械が読める印を付けて、あとから検出できるようにしなさい、っていう義務が書かれてるの
![two penalty bars side by side with the taller one highlighted. Labels in English: 'up to EUR 15 million', 'up to 3% of total worldwide annual turnover', 'whichever is higher'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/030_visual.png)
- 🦜 きなこ：違反すると最大1,500万ユーロ、または全世界の年間売上高の3%。どちらか高いほうが制裁金として科されることになってるの
- 🦜 きなこ：そうなの。だからこれ、Anthropicが善意で付けてる印じゃなくて、付けないと会社のお金がごっそり飛ぶ、っていう義務なんだよ
![horizontal timeline strip with two markers. Labels in English: '2 Aug 2026 - transparency obligations apply', 'Dec 2026 - grace period ends for generative AI systems placed on the market before 2 Aug 2026 (marking duty only)'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/033_visual.png)
- 🦜 きなこ：ただ、8月2日より前から市場に出てるAIには、印を付ける義務だけ2026年12月まで猶予が付いてるの。それ以外の義務は、もう始まってるんだよ

## 『見えない印』は本当に信用できるのか

![Before/after diagram: text panel with a glowing embedded watermark signal on the left, an arrow labeled 'paraphrase / back-translation' in the middle, and the same text with the watermark signal gone on the right](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/037_visual.png)
- 🦜 きなこ：それが消えちゃうの。文章を同じ意味のまま別の言い方に書き直す、いわゆる言い換えだね。たったそれだけで、埋め込まれた印の信号は壊れちゃうんだよ
- 🦜 きなこ：まさにそれ。意味はそのまま、単語や語順だけを入れ替える。別の言語に一度訳して、また日本語に戻すだけでも、同じように印が薄れるの
![Simple bar chart titled 'Conditional watermark removal rate after paraphrase attack': KGW 100%, Unigram 100%, SynthID-Text 98.3%](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/041_visual.png)
- 🦜 きなこ：2026年7月に出た研究だと、代表的な3つの方式を試して、攻撃前は検出できていた文章のほぼ全部から、印が消えたって報告されてるの
![Courtroom gavel icon beside a checklist of five Daubert factors, with at least two items marked as failed](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/043_visual.png)
- 🦜 きなこ：そう、冒頭で言った弱点がこれなの。しかも同じ研究は、どの透かし方式も、裁判で証拠として認められる基準を満たしてないって結論づけてるんだよ
![Caution badge reading 'PREPRINT - NOT PEER-REVIEWED' with a small note: sample size n=30](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/045_visual.png)
- 🦜 きなこ：まあ落ち着いて。今紹介した研究の多くは査読前の論文で、サンプル数も小さいの。弱点があるって方向性は学会でも共通認識だけど、数字そのものはまだ揺れてる
- 🐹 もっちー：なあきなこ、結局さ、見えへん印さえ入っとったら、AIが書いた文章かどうか一発でバレるんやろ？それやったら安心やん

## OpenAIやGoogleはどうしているのか

![Comparison table: Anthropic, OpenAI and Google - watermark coverage by content type](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/047_visual.png)
- 🦜 きなこ：実はね、OpenAIは2026年5月19日に、GoogleディープマインドのSynthIDっていう透かし技術を採用するって発表してるの
![Diagram: SynthID adding an invisible watermark layer onto an AI-generated image](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/049_visual.png)
- 🦜 きなこ：ざっくり言うと、AIが作った画像に人の目じゃ気づけない印の層をそっと重ねる仕組み。ChatGPTやCodex、API経由の画像が対象なの
![Timeline: 2026-05-19 images covered, 2026-07-31 audio added, text not covered](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/051_visual.png)
- 🦜 きなこ：そこが一番まちがえやすいところ。印が乗るのは画像で、7月31日には対応する音声にも広がったけど、テキストは対象に入ってないの
![Diagram: C2PA signed provenance metadata attached to an image file](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/053_visual.png)
- 🦜 きなこ：そう。そして画像やファイルには、C2PAっていう別の仕組みが使われてて、いつ誰がどう作ったかの記録を署名つきで添えるんだよ
![Side-by-side: metadata attached outside the file versus a watermark woven into the text](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/055_visual.png)
- 🦜 きなこ：その例えでばっちり。Claudeも画像やファイルはC2PAの記録で扱ってて、文章そのものに織り込む透かしとは仕組みが違うの
![Summary table: text watermark by Claude versus image and audio by SynthID and C2PA](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/056_visual.png)
- 🦜 きなこ：だから今は、画像と音声はSynthIDやC2PA、文章の中に印を織り込むのはClaudeが先に踏み込んだ、っていう住み分けになってる

## まとめ

![Two-column summary card: left column shows confirmed points (invisible text watermark rollout, EU rule compliance), right column shows unresolved points (public detection tool, robustness data)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V275/057_visual.png)
- 🦜 きなこ：じゃあ、今日のまとめ。Claudeが書いた文章には、8月2日から目に見えない印が入るようになった
- 🐹 もっちー：理由は、EUのルールで義務になったから。守らないと、とんでもない額の罰金がかかるって話だったよね
- 🦜 きなこ：そう。ただ、大きく書き換えたり、別の言語に翻訳したりすると、その印は消えちゃうことがあるって研究でも示されてる
- 🐹 もっちー：ってことは、印がないからって人間が書いたとは言い切られへんのやな。ややこしいなあ

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*