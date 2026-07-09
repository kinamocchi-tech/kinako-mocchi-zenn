---
title: OpenAIの新音声AI「GPT-Live」は本当にすごい？開発者向けAPIがまだない理由【解説記事】
emoji: 🤖
type: tech
topics:
- voicevox
- ai
- gpt-live
- chatgpt
- llm
published: true
---

# OpenAIの新音声AI「GPT-Live」は本当にすごい？開発者向けAPIがまだない理由

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [OpenAIの新音声AI「GPT-Live」は本当にすごい？開発者向けAPIがまだない理由](https://youtu.be/W8-uVZYl7AI)
:::

## この記事で分かること

- 🐹 もっちー：なあきなこ、AIと喋るのってさ、いつも「どっちが先に喋るか」の順番待ちみたいで、ぎこちなくない？
- 🐹 もっちー：え、順番待ちがなくなるってどういうこと？
- 🦜 きなこ：相槌を打ちながら聞いたり、話を遮ったり、考える間を自然に置いたり。人間同士の会話みたいになったの。今日はその仕組みと、まだできないことまで全部見せるね
- 🦜 きなこ：そう、発表は華やかだけど、実はまだ触れない人もいるの。順番に見ていこう

## フルデュプレックスとは何か

!["Full Duplex" text displayed boldly and dramatically on screen](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/012_visual.png)
- 🦜 きなこ：じゃあ本題いくね。GPT-Liveの一番の特徴は『フルデュプレックス』っていう仕組みなの
![電話とトランシーバーのイラストが並んで表示される](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/014_visual.png)
- 🦜 きなこ：大丈夫、噛み砕いて説明するね。普通の電話とトランシーバー、この2つで例えると一発で分かるよ
!["Half-Duplex (Turn-based)" text with a diagram showing characters speaking in alternating turns](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/016_visual.png)
- 🦜 きなこ：そうそう。トランシーバーは片方が話してる間、もう片方は黙って聞くだけ。喋る番が交互に来るこの方式が『半二重』って呼ばれてるの
![従来の音声AIのターン制（半二重）応答フロー図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/018_visual.png)
- 🦜 きなこ：実はね、今までの音声AIも構造は同じだったの。こっちが話し終わるまでAIは待って、AIが話してる間はこっちも黙って聞くしかなかった
!["Full-Duplex" text with a diagram switching to simultaneous speech](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/020_visual.png)
- 🦜 きなこ：まさにそういうこと。でもGPT-Liveはそこが違うの。電話と同じ『全二重』方式に切り替わったんだよ
![Key point text: "Backchannel, interrupt, or silence — decided many times per second"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/022_visual.png)
- 🦜 きなこ：そうなの。GPT-Liveは音声の入力と出力を同時に処理してて、相槌を打つか、話の途中で割り込むか、それとも黙って待つか、そういう判断を1秒間に何度もしてるんだよ

## GPT-5.5への委任という設計思想

![GPT-Liveの背後にGPT-5.5が控えているシルエットを重ねたイメージ図を表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/031_visual.png)
- 🦜 きなこ：そう、その正体がGPT-5.5なんだよ。GPT-Liveは会話に特化した軽量モデルで、その裏にちゃっかりGPT-5.5が控えてるってわけ
![Conditional branch icon showing "Delegate only for complex questions or calculations"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/032_visual.png)
- 🦜 きなこ：難しい質問とか複雑な計算が来たときだけ、バックグラウンドでこっそりGPT-5.5に処理を投げて、答えが出たらすぐにまた自然な会話へ戻す仕組みなんだよ
![受付カウンターに立つGPT-Liveの奥に、専門家オフィスのGPT-5.5がいるイラストで役割分担を図示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/034_visual.png)
- 🦜 きなこ：たとえるなら受付係と専門家の分担だね。GPT-Liveが受付でお客さんの話をまず聞いて、難しい相談だけこっそり奥の専門家GPT-5.5に回して、答えをもらってくるの
![ウェブ検索や複雑な推論の質問が来たら矢印がGPT-5.5へ伸び、答えが会話に戻ってくる処理フロー図を表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/036_visual.png)
- 🦜 きなこ：たとえばウェブ検索が必要な質問とか、頭を使う複雑な推論が来たときだけ、その場でGPT-5.5にこっそり処理を任せて結果だけ会話に返す設計なの
![委任中も相槌で間を持たせる会話継続の仕組みを示す図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/038_visual.png)
- 🦜 きなこ：そこがGPT-Liveの上手いところで、委任してる間も相槌を打ちながら間を持たせて、会話を途切れさせないように工夫されてる設計なんだよ
- 🦜 きなこ：そういうこと。しかも呼んでる間も会話が止まらないように工夫されてるから、待たされてる感じもしないんだよ

## まだ使えない場面——API非公開という制約

![Text caption showing "Developer API not yet available"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/043_visual.png)
- 🦜 きなこ：そうなの。API非公開だから、今できるのはあくまでChatGPTユーザーとしての体験だけで、開発者として自分のアプリに組み込める段階じゃないんだよね
![Text info showing "API: release date TBD, price undisclosed"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/045_visual.png)
- 🦜 きなこ：そう。開発者向けAPIは発表の時点でまだ公開されてなくて、サインアップフォームで登録するだけの状態なの。価格も提供時期も、いっさい非公開なんだよね
![Contrast summary caption: "Experience changes" vs "Development still ahead"](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/051_visual.png)
- 🦜 きなこ：そこまで悲観することはないよ。ChatGPTを使ってる人にとっては会話の体験がちゃんと変わるから。ただ、動画制作に組み込みたい開発者としては、まだ待ちの段階ってだけなの
- 🦜 きなこ：そういうこと。API公開のニュースは、また続報として追いかけていきたいね
- 🐹 もっちー：はぁ！？ワイらみたいな動画クリエイターとか開発者は、API、まだ使われへんってこと！？さっきまでの盛り上がりが一気にしぼむやん！
- 🐹 もっちー：え…価格も時期もまだ決まってないの？サインアップフォームに登録するだけって、正直ちょっと拍子抜けの発表だなって思っちゃう

## まとめ

![GPT-Live-1／miniの提供範囲まとめ図（ChatGPTユーザーは利用可・開発者APIは未提供）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V246/054_visual.png)
- 🦜 きなこ：まとめると、GPT-Liveはフルデュプレックスで会話がぐっと自然になった。でも開発者向けAPIはまだ非公開で、価格も未定なの
- 🐹 もっちー：今できることとまだのこと、整理できてよかった！これ保存しとこ！
- 🦜 きなこ：実際どこまで自然になったかは、触ってみた人の感想次第だと思うんだよね。みんなはどう感じた？
- 🐹 もっちー：たしかに、価格も提供時期も決まってないんじゃ、判断材料が足りないもんね

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*