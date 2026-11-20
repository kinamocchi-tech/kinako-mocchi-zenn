---
title: Gemini 4 Neonの単価はCarbonより高いのに12月に逆転する理由。ベンチの読み方も整理【解説記事】
emoji: 🤖
type: tech
topics:
- voicevox
- ai
- gemini4neon
- gemini
- gemini4carbon
published: true
---

# Gemini 4 Neonの単価はCarbonより高いのに12月に逆転する理由。ベンチの読み方も整理

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [Gemini 4 Neonの単価はCarbonより高いのに12月に逆転する理由。ベンチの読み方も整理](https://www.youtube.com/watch?v=mmX_8Ak6FA4)
:::
@[youtube](mmX_8Ak6FA4)

## この記事で分かること

- 🐹 もっちー：ねえきなこ、Geminiの新しいやつNeonって、Carbonより安くなったの？
- 🐹 もっちー：逆転するんや！でもそれ、単価だけの話だよね？
- 🦜 きなこ：そう。今日は料金、使える場所、ベンチマークの読み方を、公式ページだけで整理するね

## Neonの立ち位置と使える場所

![図: Carbon（長時間・最難関）／Neon（バランス）／Hydrogen（速い日常）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/012_visual.png)
- 🦜 きなこ：Googleの説明だと、Carbonは一番重い長時間の仕事向け。Hydrogenは速い日常の実行向け。Neonはその間で、深さと効率のバランスを取る役なの
![テロップ: Carbon 10/28発表・11/10 API提供 → Neon 11/18](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/013_visual.png)
- 🦜 きなこ：Carbonは10月28日に発表されて、APIは11月10日に有料の開発者と企業向けに出たばかり。発表から約3週間で、Neonが出た形なの
![表: Gemini API（有料）／Gemini for business／Antigravity・アプリ（AI Pro・Ultra）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/015_visual.png)
- 🦜 きなこ：APIはGoogle AI StudioのGemini API、有料枠。Gemini for businessでも使えるよ
- 🦜 きなこ：GeminiアプリとAntigravityは、有料のAI ProかUltraの加入者が対象なの
![テロップ: 無料枠 Neon なし／Hydrogen あり](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/018_visual.png)
- 🦜 きなこ：価格ページでは、Neonに無料枠はないの。ちなみにHydrogenには無料枠があるよ
![テロップ: Neon for cyber＝Fairwind の承認済み防御者向け（日付は未記載）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/020_visual.png)
- 🦜 きなこ：Neon for cyberは、Fairwind Programの承認された防御者に、数日のうちに順次提供するって書かれてるの。日付までは書かれてないよ

## 単価の読み方

![表: Neon $3/$15/$0.15／Hydrogen $1.50/$7.50（100万トークンあたり・標準）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/028_visual.png)
- 🦜 きなこ：標準料金は100万トークンあたりね。Neonが入力3ドル、出力15ドル、キャッシュ入力が0.15ドル。Hydrogenは1ドル50セントと7ドル50セントなの
![表追記: Carbon 〜11/30 $2/$10 → 12/1〜 $4/$20／Neon Batch・Flex $1.50/$7.50](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/029_visual.png)
- 🦜 きなこ：Carbonは11月30日まで2ドルと10ドル、12月1日から4ドルと20ドル。BatchとFlexなら、Neonは1ドル50セントと7ドル50セントで、標準のちょうど半分だよ
![表: Priority Neon $5.40/$27／Carbon 〜11/30 $3.60/$18 → 12/1〜 $7.20/$36](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/030_visual.png)
- 🦜 きなこ：急ぎの処理向けのPriorityだと、Neonは5ドル40セントと27ドル。Carbonは11月中が3ドル60セントと18ドル、12月から7ドル20セントと36ドルなの
![テロップ: 32%＝タスクあたりコスト（Google報告値）≠ 単価差](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/032_visual.png)
- 🦜 きなこ：その32%は単価じゃなくて、high設定でタスクひとつを終えるまでの費用なの。Artificial AnalysisをGoogleが紹介している数字で、第三者の再現は確認できてないよ
- 🦜 きなこ：そう。単価が安くても、使うトークンが多ければ総額は上がるの。11月中はCarbonのほうが単価は安いから、用途で分かれるね
![表: 試算（入力100万＋出力10万トークン）Neon $4.50／Carbon 〜11/30 $3.00／Carbon 12/1〜 $6.00](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/036_visual.png)
- 🦜 きなこ：入力100万トークン、出力10万トークンを使うと仮定した、わたしの試算ね。Neonは4ドル50セント、Carbonは11月中が3ドル、12月からは6ドル

## ベンチマークの読み方

![図: 比較相手＝Claude Opus 5.5／GPT-6.2 Sol（Carbonなし）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/041_visual.png)
- 🦜 きなこ：全部じゃないの。model cardの比較表は、Claude Opus 5.5とGPT-6.2 Solとの比較で、Carbonは入ってないよ
![表: AA Intelligence Index 61 / 59 / 57（Google報告値）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/042_visual.png)
- 🦜 きなこ：総合の指数では、Artificial AnalysisのIntelligence Indexが、Neonが61、Opus 5.5が59、GPT-6.2 Solが57なの
![表: 勝ち＝Vals 70.9% / AutomationBench 56.3%（Google報告値）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/044_visual.png)
- 🦜 きなこ：勝ってる例は、Vals Indexが70.9%で、Opus 5.5が70.1%、GPT-6.2 Solが66.1%。AutomationBenchは56.3%に対して、42.5%と41.3%
![表: 負け＝Terminal-bench 4.1 65.2%<65.8% / FrontierCode 46.2%<47.3% / Chartography 73.5%<75.1%](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/045_visual.png)
- 🦜 きなこ：負けてる例もあるの。Terminal-bench 4.1は65.2%で、Opus 5.5が65.8%。FrontierCode 2.0は46.2%に対して47.3%
- 🦜 きなこ：ChartographyはGPT-6.2 Solの75.1%が上なの
![表: SWE-sweep provider harness 39.0% vs 10.1%／mini-SWE 12.8% vs 3.6%](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/048_visual.png)
- 🦜 きなこ：SWE-sweepは評価の仕方次第なの。provider harnessだと39.0%で、Opus 5.5が10.1%

## 試す前に知っておくこと

![テロップ: 思考レベル4段階（既定 high／最上位 xhigh）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/054_visual.png)
- 🦜 きなこ：思考レベルは4段階で、既定はhigh、いちばん上がxhigh。残り2つの名前は、発表の本文には書かれてないの
- 🦜 きなこ：長い作業向けに、同じファイルの読み直しを減らしたり、進捗を共有したりする仕組みもうたってるよ
![テロップ: 安全性の数値はすべてGoogle報告値](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/057_visual.png)
- 🦜 きなこ：不正行為の評価で2.45%、エージェントの誠実性評価で99.2%、間接プロンプトインジェクションは最上位設定で攻撃成功0.0%。どれもGoogleの報告値なの
![テロップ: 知識の期限 2026年3月／詳細レポートは coming soon](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/058_visual.png)
- 🦜 きなこ：限界欄には、ハルシネーションや知識が古い領域があると書いてあるよ。知識の期限は2026年3月で、安全性の詳細レポートはcoming soonなの
![テロップ: under-service 43〜56%減／overreach 15〜35%減（Google報告値）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/059_visual.png)
- 🦜 きなこ：Carbonと比べて、頼まれた内容に足りない対応が43〜56%、やりすぎが15〜35%減ったとも書いてるよ。努力レベルで幅があって、これもGoogleの報告値なの
- 🦜 きなこ：長い仕事を任せたい開発者や、費用を測りたい人。まず自分のタスクをCarbonと同じ条件で比べるのがいいね

## まとめ

![まとめ: ①単価は12/1に逆転 ②32%はタスクあたり ③ベンチはGoogle報告値](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/067_visual.png)
- 🦜 きなこ：まとめると、Neonの単価は11月中はCarbonより高いけど、12月1日から逆転するの
- 🐹 もっちー：ベンチは勝ち負けがあって、全部Googleの報告値だから、自分で試すのが大事だね
![テロップ: 安全性の詳細レポート＝coming soon](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V328/069_visual.png)
- 🦜 きなこ：あと、安全性の詳細レポートはまだcoming soonだから、続報が出たら確認したいね
- 🦜 きなこ：飼い主もタブレットで料金表を見比べて、固まってたよ

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*