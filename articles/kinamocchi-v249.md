---
title: 賢くなったAIが嘘つきに？Grok 4.5が暴くベンチマークの落とし穴【解説記事】
emoji: 🤖
type: tech
topics:
- voicevox
- ai
- grok
- xai
- spacex
published: true
---

# 賢くなったAIが嘘つきに？Grok 4.5が暴くベンチマークの落とし穴

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [賢くなったAIが嘘つきに？Grok 4.5が暴くベンチマークの落とし穴](https://www.youtube.com/watch?v=d5LthZab6AU)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、聞いてや！Grok 4.5っていう新モデルが出て、なんかめっちゃ賢くなったらしいで！最強ちゃう？
- 🐹 もっちー：え、待って。賢くなったのに、間違いも倍に増えてるの？どういうこと、意味わからないよ
![正答率↑とハルシネーション率↑が同時に起きている矛盾を強調するテロップ（賢くなったのに間違いも倍増）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/006_diagram.png)
- 🦜 きなこ：そう。正答率はちゃんと上がったのに、でたらめを言う頻度まで倍に…この矛盾、変だと思わない？
- 🐹 もっちー：思うよ！賢くなったんだったら、間違いは減るのが普通じゃないの？なんか話が逆だよ

## Grok 4.5 とは何者か（SpaceXAI・改名・Cursor買収）

![タイムライン図③: 2026年7月8日 Grok 4.5発表（改名後の初モデル）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/020_diagram.png)
- 🦜 きなこ：その通り。改名のすぐ後、2026年7月8日に発表されたのが、この新生SpaceXAIの初モデル、Grok 4.5なんだよ
![マスク氏の発言カードに英語ラベル 'Opus-class model' を表示し、下に 'Self-reported claim, not independent evaluation' と注記する](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/022_diagram.png)
- 🦜 きなこ：しかもね、イーロン・マスク自身の言葉では、Grok 4.5は『Opusクラスのモデル』なんだって
- 🦜 きなこ：ただここは要注意。それはマスク本人のX投稿での表現で、つまり企業側の自己申告なの。独立した第三者評価じゃないんだよ
![コーディング特化を打ち出すGrok 4.5のイメージ（コードエディタ画面）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/026_diagram.png)
- 🦜 きなこ：そう。だから話半分で聞くのが正解。しかもGrok 4.5は、コーディング特化を強く打ち出してるの
![図: SpaceXAI →（買収）→ Cursor（親会社 Anysphere・コード生成ツール）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/028_diagram.png)
- 🦜 きなこ：SpaceXAIがね、人気のコード生成ツールCursor、その親会社のAnysphereを買収したの。だからコーディングに力が入ってるんだね
![$60Bカード: 約600億ドル（$60B）全株式取引・2026年6月16日発表](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/030_diagram.png)
- 🦜 きなこ：約600億ドル、$60Bもの全株式取引なの。2026年6月16日の発表だよ。60億ドルじゃなくて、その10倍なの

## 性能は本物（Intelligence Index・正答率・激安価格）

![Artificial Analysis Intelligence Indexの総合スコアバーを表示。Grok 4.5のバーをハイライト](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/035_diagram.png)
- 🦜 きなこ：まずは性能から見ていくね。Artificial Analysis、通称AAっていう第三者機関が出してる知能指数、Intelligence Indexで測るの
![比較バー: Grok 4.5=54点 vs 前世代Grok 4.3=38点、差分+16点を強調表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/037_diagram.png)
- 🦜 きなこ：近いかも。そのIndexで、Grok 4.5は54点。前世代のGrok 4.3が38点だったから、一世代で+16点も跳ね上がったの
![Intelligence Index上位モデルのリーダーボードを表示。Grok 4.5が全体4位の位置をハイライト](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/039_diagram.png)
- 🦜 きなこ：そうなの。しかもAAの発表記事だと、この54点は最新モデルがずらっと並ぶ中で全体4位。トップ集団のすぐ下なんだよ
![正答率グラフ: AA-Omniscience 正答率 35%→52%への上昇を矢印付きで表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/042_diagram.png)
- 🦜 きなこ：次は正答率。AA-Omniscienceっていう知識テストで、Grok 4.5の正答率は35%から52%へ。半分を超えてきたの
- 🦜 きなこ：そういうこと。だから、性能が上がったこと自体は本当なの。ここはもう、私も素直に認めるしかないの
![価格比較表: Grok 4.5のAPI料金と上位モデルの料金を並べた表を表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/045_diagram.png)
- 🦜 きなこ：で、もっちーが一番好きそうな話にいくね。お値段なんだけど、これがまた笑っちゃうくらい激安なの

## トレードオフの正体（ハルシネーション率25%→54%）

- 🦜 きなこ：そう思うよね。私も最初はまったく同じことを思ってた。賢いモデルなら安心できる、って。でもね、そこに大きな落とし穴が隠れてたの
![AA-Omniscienceの正答率が35%→52%に上昇したバーを表示（前セクションの復習・緑色）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/055_diagram.png)
- 🦜 きなこ：覚えてる？正答率は35%から52%に上がった。ざっくり、当たる割合が半分近くまで増えたってこと。ここだけ見れば、文句なしの良いニュースなの
![同じレポート内のもう一つの指標として英語ラベル 'Hallucination Rate' をハイライト表示する](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/056_diagram.png)
- 🦜 きなこ：でもね、同じレポートの中に、正答率とぴったり寄り添うように、こっそり一緒に動いた数字がもう一つあるの。ハルシネーション率
![ハルシネーションの定義を図解し、英語ラベル 'Hallucination = confident wrong answer' を表示する](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/058_diagram.png)
- 🦜 きなこ：ちょっと違うの。ハルシネーションは、自信たっぷりに間違えること。本当は知らないのに、知ってるフリして、堂々と嘘を言い切っちゃうことなの
![ハルシネーション率が25%→54%へ倍増したことを赤色で強調表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/059_diagram.png)
- 🦜 きなこ：その自信満々の間違いが、Grok 4.5では25%から54%へ。正答率が伸びたのと、まさに同時に、倍以上へ跳ね上がってたの
- 🦜 きなこ：そう思うよね。その反応で正しいの。賢くなったはずなのに、嘘だけ倍増する——確かに、頭では矛盾にしか見えない。でもね、ちゃんと理由があるの

## なぜ賢いほど自信満々に間違えるのか（メカニズム）

![テスト用紙のたとえ図: 空欄=0点 vs とりあえず埋める=当たれば加点、を対比表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/074_diagram.png)
- 🦜 きなこ：もっちー、今すごく大事なこと言ったよ。それがハルシネーションが増える正体そのものなの
- 🦜 きなこ：その『空欄より埋めた方が得』っていう感覚を、AIの採点方法がそっくりそのまま作り出しちゃってるの
![OpenAI論文引用カードに英語ラベル 'Training & evaluation reward guessing over admitting uncertainty' を表示する（出典: why-language-models-hallucinate）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/077_diagram.png)
- 🦜 きなこ：そうなの。OpenAIの研究が、学習と評価は『わからない』と認めることより…
- 🦜 きなこ：『自信を持って当てずっぽうで答える』方に高い点をつけてる、ってはっきり指摘してるんだよ
- 🦜 きなこ：だからモデルは『良い受験者』になるよう鍛えられていて、迷ったら黙るより推測した方が点が伸びるの
![2択の図を並べて表示し、左に英語ラベル 'Score goes up'、右に 'Wrong answers stay confident' を配置する](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/081_diagram.png)
- 🦜 きなこ：でしょ？その戦略、確かにテストの点数は上がるの。でも外したときは『自信満々の誤答』が残っちゃう

## ベンチマークの読み方（4位/9位・ハーネス不一致・自己申告）

![同じ54点のスコアが、左のボード（英語ラベル 'AA announcement = 4th'）と右のボード（英語ラベル 'Full leaderboard = 9th'）に並んで表示される](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/092_diagram.png)
- 🦜 きなこ：いいところに気づいたね。実はね、同じ54点なのに、見る場所で4位にも9位にもなるの
- 🦜 きなこ：どっちも本当なんだよ。AAの発表記事は、Fable5・GPT-5.5・Opus4.8と並べて『4位』ってフレーミングしてるの
![186モデルが並ぶ全体リーダーボード（Intelligence Index v4.1）でGrok 4.5の行に英語ラベル '9th' のハイライトが表示される](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/095_diagram.png)
- 🦜 きなこ：でも全モデルのリーダーボード、186個並んだ表で見ると9位。同じスコアでも、どの土俵で比べるかで順位が変わるの
![落とし穴①として英語テロップ 'Rank depends on which leaderboard (4th vs 9th)' が表示される](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/097_diagram.png)
- 🦜 きなこ：そう、それが落とし穴の1つめ。順位は『どのランキングか』を見ないと、意味が変わっちゃうの
!['Grok 4.5 $2.49 / Fable 5 $11.80 / GPT-5.5 $5.07' の価格比較表の下に英語注記 'Different harness per model — not an apples-to-apples comparison' が付く](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/099_diagram.png)
- 🦜 きなこ：安いのは本当。でもね、あの$2.49と、Fable5の$11.80って、実は別々のハーネスで測った数字なの
- 🦜 きなこ：エージェントの土台のことだよ。GrokはGrok Build、Fable5はClaude Code、GPT-5.5はCodex。全部別なの

## まとめ

![まとめタイトルとして英語テロップ 'Grok 4.5 = the trade-off between smarts and hallucination' を表示する](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/113_diagram.png)
- 🦜 きなこ：じゃあ今日のまとめね。Grok 4.5は、賢さとハルシネーションが一緒に上がる、そんなトレードオフを持ったモデルだったの
- 🐹 もっちー：賢くなったら間違いも減るって思い込んでたけど、そうとは限らないんだね
![実用の3つのコツ ①1つの数字で判断しない（知能指数だけでなくハルシネーション率も見る）を番号付きテロップで表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/115_diagram.png)
- 🦜 きなこ：だから実用のコツを3つ渡すね。1つ目は、1つの数字で判断しないこと。知能指数だけじゃなく、ハルシネーション率もセットで見るの
![番号テロップ2として英語ラベル 'Read the benchmark conditions (harness, which view)' を追加する](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/117_diagram.png)
- 🦜 きなこ：2つ目は、ベンチマークの『条件』を読むこと。どんなハーネスで、どのビューを見た結果なのか、そこまで確認するの
![番号テロップ3として英語ラベル 'For important tasks, always verify — AI can be confidently wrong' を追加する](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V249/119_diagram.png)
- 🦜 きなこ：3つ目は、重要な用途では『AIは自信満々に間違える』前提で必ず検証すること。ここが一番大事なの

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*