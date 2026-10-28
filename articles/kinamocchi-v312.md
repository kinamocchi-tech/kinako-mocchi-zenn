---
title: GPT-6.1 Terra登場。半額の画面操作AIで何を任せる？Luna・Sol・Astraの選び方【解説記事】
emoji: 🤖
type: tech
topics:
- voicevox
- ai
- terra
- computeruse
- gpt-6astra
published: true
---

# GPT-6.1 Terra登場。半額の画面操作AIで何を任せる？Luna・Sol・Astraの選び方

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [GPT-6.1 Terra登場。半額の画面操作AIで何を任せる？Luna・Sol・Astraの選び方](https://www.youtube.com/watch?v=Zc-4ZOx1buw)
:::
@[youtube](Zc-4ZOx1buw)

## この記事で分かること

- 🐹 もっちー：ねえきなこ、GPT-6.1 TerraってSolの半額なんでしょ？ どうせ性能も半分くらいなんでしょ？
- 🐹 もっちー：えっ、ほぼSolと同じ場所におるやん！ ほな半額で、ええとこ取りちゃうん？
- 🦜 きなこ：そこは半分だけ本当なの。今日は任せ方と、選び方まで見るよ
- 🐹 もっちー：え、残りの半分って、何があるの？

## Terraの位置づけと価格

![4階級カード：Luna → Terra → Sol → Astra（安い順）／Terra＝中位](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/012.png)
- 🦜 きなこ：OpenAIのモデルは、安い順にLuna、Terra、Sol、Astraの4階級なの
- 🦜 きなこ：Terraは2番目で、報道では日常の仕事向けと説明されているよ
![価格表（Standard・100万トークンあたり 入力／出力）：Luna 0.10ドル／0.50ドル、Terra 1ドル／5ドル、Sol 2ドル／10ドル、Astra 10ドル／50ドル](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/014.png)
- 🦜 きなこ：100万トークンあたりの価格は、Lunaが入力10セントと出力50セント。Terraが1ドルと5ドル。Solが2ドルと10ドル
- 🦜 きなこ：Astraが10ドルと50ドルだよ
![提供カード：ChatGPT Work・Codex（Plus／Pro／Enterprise／Edu）、API：gpt-6.1-terra（OpenAIの説明）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/017.png)
- 🦜 きなこ：使える場所は、OpenAIによると、ChatGPT WorkとCodexで、Plus、Pro、Enterprise、Eduのユーザーなの
- 🦜 きなこ：開発者はAPIでgpt-6.1-terraを指定するよ

## 画面操作で何を任せられるか

![仕組み図：モデル（GPT-6.1 Terra など）→（操作リスト）→ アプリが実行 →（スクリーンショット）→ モデル、の繰り返し](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/027.png)
- 🦜 きなこ：OpenAIのガイドだと、モデルがクリックや入力の操作リストを返すの。アプリ側がそれを実行して、画面のスクリーンショットを返す
![対応ツール：Terra＝computer_use に対応（Responses API・公式モデルページ）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/030.png)
- 🦜 きなこ：Terraはこのcomputer useのツールに対応していると、公式のモデルページに書いてあるよ
![確認カード：Terra固有の画面操作ベンチ（OSWorldなど）は、公式で確認できていない](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/031.png)
- 🦜 きなこ：ただ、ガイドの例に使われているのはSolとAstraなの
- 🦜 きなこ：Terraでの公式な測定値、たとえばOSWorldの数字は、見つけられなかったよ
- 🦜 きなこ：OpenAIは、画面を理解して、アプリをまたいで操作できると説明しているの。ただ、数字で比べられる材料は、今のところ少ないんだよ
![安全の要点（公式ガイド）：①購入・送信・削除の前に人が確認 ②隔離ブラウザ／仮想マシン ③許可するサイトを限る ④認証情報を画面に出さない](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/036.png)
- 🦜 きなこ：ガイドが求めるのは、まず確認なの。購入、データの送信、削除の前には、人が確認を挟む。使うのは隔離したブラウザや仮想マシン

## 単価とベンチマークの読み方

![対比カード：トークンの単価 ≠ 1タスクの費用（使うトークン量で変わる）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/045.png)
- 🦜 きなこ：それが違うの。トークンの単価と、1つの仕事にかかる費用は別物なんだよ
- 🦜 きなこ：同じ仕事でも、モデルや考える強さで、使うトークンの量が変わるからね
- 🦜 きなこ：第三者のArtificial Analysisは、最大effortの1タスクで、Terraが0.40ドル、GPT-5.6 Terraが1.40ドルと報告しているの
![注記カード：知能指数でコスパ最適は低〜中effort（Artificial Analysis）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/052.png)
- 🦜 きなこ：しかも同社は、知能指数で見ると、考える強さが低めか中くらいのときがコスパの最前線だと書いているよ
![【OpenAI自己申告】Terminal-Bench 4.0（最大effort）：GPT-6.1 Terra 50.3%／GPT-5.6 Terra 21.5%](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/054.png)
- 🦜 きなこ：ここからは、OpenAI自身が測った数字だよ
- 🦜 きなこ：Terminal-Bench 4.0を最大effortで解いた割合は、Terraが50.3%、GPT-5.6 Terraが21.5%なの

## どれを選ぶか

![選び方（OpenAIの説明）：複雑なコーディング・深い調査＝Sol／Astra、日常の仕事＝Terra](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/070.png)
- 🦜 きなこ：OpenAIは、複雑なコーディングや深い調査には、SolかAstraを勧めているそうなの。日常の仕事向けがTerraという説明だよ
![Solのモデルページ：複雑なコーディング・computer use・専門的な仕事向け](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/071.png)
- 🦜 きなこ：Solのページにも、複雑なコーディング、computer use、専門的な仕事向けと書いてあるの
- 🦜 きなこ：画面操作は、Solも得意分野なんだよ
![見立てカード（見立てであり公式情報ではない）：失敗の被害が大きい・難しい＝Sol寄り／量をこなす画面操作＝Terraを試す](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/074.png)
- 🦜 きなこ：間違えたときの被害が大きい仕事や、難しい実装なら、そうだね。でも、量をこなしたい画面操作なら、半額のTerraを試す価値があるの
![単価の比較（100万トークンあたり）：Luna 入力0.10ドル・出力0.50ドル、Terra 入力1ドル・出力5ドル](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/077.png)
- 🦜 きなこ：Lunaは、単価がTerraの10分の1なの。軽い仕分けで試す手はあるけど、画面操作を任せられるかは、公式に数字がないんだよ
![料金モードカード：Batch・Flex＝半額（Terra 入力0.50ドル／出力2.50ドル）、Fast＝2倍（入力2ドル／出力10ドル）、入力27万2千トークン超＝割増（入力2ドル／出力7.50ドル）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/078.png)
- 🦜 きなこ：お金を抑える方法もあるよ。バッチとFlexは半額。逆にFastは2倍。入力が27万2千トークンを超えると、割増になるの

## まとめ

![まとめカード：①Solの半額（1ドル／5ドル）②第三者の指数はSolの4ポイント下 ③画面操作に対応（確認と隔離が前提） ④数字の多くはOpenAI自己申告](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/081.png)
- 🦜 きなこ：最後にまとめるね。Terraは、Solの半額で、第三者の指数でもSolに近い位置にいるの
- 🦜 きなこ：画面操作に対応していて、確認と隔離を前提に使うものなんだよ
- 🦜 きなこ：でも、数字の多くはOpenAI自身のもの。Terraでの画面操作の公式な測定値は、まだ見つかっていないの
![行動カード：同じ依頼を“今のモデル”と“Terra”で試し、やり直しの回数を数える（1つの作業だけ）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V312/084.png)
- 🦜 きなこ：今日やってほしいのは1つだけ。いつもの作業を1つ選んで、今のモデルとTerraに同じ頼み方をして、やり直しの回数を数えてみて

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*