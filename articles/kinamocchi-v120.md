---
title: AIインフラ覇権戦争の本質！Anthropic × CoreWeaveの真実を徹底解説【解説記事】
emoji: 🤖
type: tech
topics:
- voicevox
- ai
- coreweave
- nvidia
- gpu
published: true
---

# AIインフラ覇権戦争の本質！Anthropic × CoreWeaveの真実を徹底解説

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [AIインフラ覇権戦争の本質！Anthropic × CoreWeaveの真実を徹底解説](https://www.youtube.com/watch?v=hkNK6Vd69Nc)
:::

## この記事で分かること

- 🦜 きなこ：今日はね、モデルの賢さ競争の裏で起きてる、血みどろのGPU覇権戦争の話をするね
- 🦜 きなこ：じゃあまずは、CoreWeaveっていう会社がどこから来たのか、その正体から見ていこっか

## CoreWeaveの出自 — 暗号資産マイナーからAIインフラ王者へ

![設立: 2017年 / 本拠地: ニュージャージー州](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/017_coreweave_founded.png)
- 🦜 きなこ：CoreWeaveはね、2017年にニュージャージー州で生まれた会社なの
![旧社名: Atlantic Crypto Corp.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/018_coreweave_old_name.png)
- 🦜 きなこ：でね、ここからが面白いんだけど。当時の社名はCoreWeaveじゃなくて、Atlantic Crypto Corp.っていう名前だったの
![創業者3人: コモディティ・エネルギー先物トレーダー出身](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/020_founders.png)
- 🦜 きなこ：そう、ぜんぜん違うの。しかもね、創業者3人は全員、コモディティとかエネルギー先物のトレーダー出身なんだよ
![2017-2018: イーサリアム採掘で大もうけ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/023_ethereum_mining.png)
- 🦜 きなこ：最初はね、イーサリアムの採掘で大もうけしたの。2017年から2018年の仮想通貨ブームに乗ってね
- 🦜 きなこ：マイニングするにはGPUが大量にいるから、ものすごい数のGPUを買い集めてたの
![2018-2019: クリプトウィンター — 仮想通貨市場崩壊](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/026_crypto_winter.png)
- 🦜 きなこ：でもね、いいことばっかりじゃなかったの。2018年から2019年、クリプトウィンターが来て仮想通貨市場が大崩壊したんだよ

## AWSじゃダメな理由

![AWSではダメな3つの理由](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/047_aws_three_reasons.png)
- 🦜 きなこ：いい質問なんだよ。実はね、AI訓練用のGPU環境としてAWSを見ると、大きく3つの問題があるの
![問題① Service Quota(GPU利用上限)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/048_service_quota.png)
- 🦜 きなこ：1つ目はService Quota。AWSにはアカウントごとにGPUの利用上限があって、増やしたかったら申請して、審査が通るのを待つ必要があるの
![問題② Goodput(実効稼働率)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/050_goodput.png)
- 🦜 きなこ：そうなの。GPUは世界中で取り合いだから、AWSも一気に大量には出せないんだよ。2つ目はGoodput、グッドプットって呼ばれる指標
- 🦜 きなこ：Goodputは、借りているGPU時間のうち、実際に計算に使えた時間の割合のこと。100時間借りて80時間しか計算できなかったらGoodputは80%なの
- 🦜 きなこ：再起動の待ち時間だったり、ハードウェア障害の復旧だったり、ネットワークが切れて訓練がやり直しになったり。大手クラウドは色んな用途と共用してるから、どうしてもロスが多いの
![CoreWeave Goodput 96% / 大手クラウド 70〜80%](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/055_goodput_comparison.png)
- 🦜 きなこ：ここがすごいところなんだよ。CoreWeaveのGoodputは96%。業界平均の70〜80%と比べて、圧倒的に高いの

## Anthropicの3レーン戦略とCoreWeave契約

![Anthropicの3レーン戦略](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/082_three_lane_strategy.png)
- 🦜 きなこ：ここがね、Anthropicの面白いところなんだよ。Anthropicは3レーン並行作戦って呼ばれる戦略を取ってるの
![①AWS Trainium / ②Google TPU / ③CoreWeave GPU](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/084_three_chips.png)
- 🦜 きなこ：そんな感じ。1番目はAWSのTrainium(トレイニウム)っていう自社チップ。2番目はGoogleのTPU。3番目はCoreWeaveのNVIDIA GPUだよ
- 🦜 きなこ：ふふっ、楽さよりも強さを取ったの。モデルの種類とか訓練の段階で使い分けて、もしどれかが止まっても他で続けられる。そういう設計なんだよ
- 🦜 きなこ：それだけじゃないの。AWSとGoogleを競争させることで、契約条件も有利に引き出せるんだよ。お互いに「うちの方が安く出せる」って言い合うから
![Anthropic × CoreWeave 大型長期契約（金額非公開）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/090_anthropic_coreweave_deal.png)
- 🦜 きなこ：AnthropicはIPO目論見書で主要顧客として記載されていて、業界でも最大規模の長期契約の一つとされてるんだよ。金額は非公開なの
![主要顧客の契約規模: OpenAI $22.4B / Meta $35.2B](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/092_contract_scale.png)
- 🦜 きなこ：比較のためにOpenAIとMetaの規模を見ると、OpenAIは224億ドル、Metaに至っては352億ドルもの契約があるって言われてるんだよ

## 次世代チップ Vera Rubin

![NVIDIA 次世代チップ: Vera Rubin](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/117_vera_rubin_chip.png)
- 🦜 きなこ：NVIDIAが開発中の次世代チップ、Vera Rubinっていうの。今のBlackwellの次の世代なんだよ
![Vera Rubin NVL72: 3,600 PFLOPS](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/119_vera_rubin_performance.png)
- 🦜 きなこ：NVL72っていう72枚のGPUを繋いだラックで、3,600ペタフロップスの計算能力なの
- 🦜 きなこ：メモリ帯域も1,580テラバイト毎秒。データをめちゃくちゃ速く動かせるの
![推論コスト: Vera Rubin = Blackwellの1/10](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/123_inference_cost.png)
- 🦜 きなこ：推論コストがBlackwellの10分の1になるの。つまり同じお金で10倍のClaudeが動かせるんだよ
- 🦜 きなこ：2026年後半に出荷予定なの
- 🦜 きなこ：NVIDIAと直接パートナーシップがあるから、最優先で確保できる立場なんだよ

## Neocloudの未来と競争

![Neocloud市場予測: 2030年 $180B](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/130_neocloud_market.png)
- 🦜 きなこ：AI専業クラウド、Neocloud市場は2030年には1,800億ドルに成長するって予測があるの
- 🦜 きなこ：Lambda Labs、Crusoe Energyとかが競合。でも規模が全然違うの
![ハイパースケーラーの反撃: AWS Trainium2 / Google TPU v5e](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V120/134_hyperscaler_response.png)
- 🦜 きなこ：ハイパースケーラーの反撃も始まってるの。AWSはTrainium2、GoogleはTPU v5eっていう独自チップを強化してるんだよ
- 🦜 きなこ：長期的にはGPUがコモディティ化するリスクもあるの
- 🦜 きなこ：普通の商品みたいに価格が下がり続けること。差別化できなくなるリスクなの
- 🦜 きなこ：NVIDIAとの最深部パートナーシップ、バックログ668億ドルから880億ドルの既存契約、そしてVera Rubinの先行確保。この3点が防衛線なの

## まとめ

- 🐹 もっちー：じゃあぼくたちみたいな普通の人はどうすればいいの?
- 🦜 きなこ：AIを使う側はインフラを意識しなくていいの。でも将来の料金やサービス品質に影響するんだよ
- 🐹 もっちー：なんか、インフラって縁の下の力持ちなんだね
- 🐹 もっちー：ねえきなこ、ぼくたちが使ってるAIも、もしかしてCoreWeaveのGPUで動いてるのかな
- 🦜 きなこ：まとめると、AIインフラの覇権争いはモデルの賢さと同じくらい重要な話なの。CoreWeaveはその要になってる会社なんだよ

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*