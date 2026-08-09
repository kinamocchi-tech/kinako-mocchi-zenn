---
title: 攻撃コード自動生成が2回→181回！Anthropicが公開しないAI防衛計画【解説記事】
emoji: 🤖
type: tech
topics:
- asl-3
- claude
- ai
- llm
- tech
published: true
---

# 攻撃コード自動生成が2回→181回！Anthropicが公開しないAI防衛計画

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [攻撃コード自動生成が2回→181回！Anthropicが公開しないAI防衛計画](https://www.youtube.com/watch?v=5KJcdSbFboE)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、AIが自分で攻撃コードを組み立てる実験、半年前は数百回試して2回しか成功しなかったのに、今は181回も成功したって知ってた？
- 🐹 もっちー：隠してる？そんなにヤバいもんなん？
- 🐹 もっちー：NATO！？なんでそんなとこまで出てくるん！
![150組織・15カ国以上・NATO参加という巨大プロジェクトの規模を示す世界地図ベースの図解(英語表記: 150 orgs, 15+ countries)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/011_global_scale.png)
- 🐹 もっちー：150組織って、なんかもう国レベルの話になってきてへん？ぼくでもついていけるかな…

## Project Glasswing 第2弾拡張の規模

![組織数の拡大(11→150)と対象国数(15カ国以上)を示す比較図解(数値表記は英語: 11 orgs to 150 orgs, 15+ countries)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/024_org_growth.png)
- 🦜 きなこ：最初は11社だけだったの。それがたった5週間で150組織・15カ国以上に広がった。14倍の拡大なんだよ
![初期ローンチパートナー(AWS/Microsoft/Google/NVIDIA等)のロゴ群表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/025_launch_partners.png)
- 🦜 きなこ：ちなみに最初の11社は、AWSやMicrosoft、Google、NVIDIAみたいな名だたるIT企業だったんだよ
![通常1年分の脆弱性発見ペースと今回5週間の対比グラフ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/027_pace_compare.png)
- 🦜 きなこ：じゃあ言い換えるね。普通なら1年かけて見つかるくらいの脆弱性が、この5週間だけで出てきたの
![CVE件数10,000件超を示す数値インパクト表示(英語表記: 10,000+ CVEs)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/029_cve_count.png)
- 🦜 きなこ：しかもただの脆弱性じゃなくて『高』か『致命的』レベルだけで1万件超え
![OSSスキャン結果の内訳を示すグラフ(23,019件中6,202件が高/致命的。英語表記で26.9%を表示)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/032_oss_breakdown.png)
- 🦜 きなこ：23,019件の脆弱性のうち、6,202件が『高』か『致命的』。全体の約26.9%だよ
![外部検証で1,752件中9割以上が有効な脆弱性と確認されたことを示すチェックマーク図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/034_external_validation.png)
- 🦜 きなこ：そこもちゃんと確認済み。外部のセキュリティ会社が1,752件を精査したら、9割以上が本物だったの

## 初期コホートとの差分と重要インフラへの拡大

- 🦜 きなこ：そう思うよね。実は電力・水道・医療・通信・半導体みたいなハードウェアが新しく加わったの
![初期コホート(IT企業中心)と第2弾(重要インフラ)の業種対比図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/043_cohort_compare.png)
- 🦜 きなこ：最初の11社はAWSとかMicrosoftみたいなIT企業中心だったから、業界の顔ぶれが一気に変わったんだよね
- 🦜 きなこ：そうなの。だからこそ今回の拡大は、単なるビジネス拡大じゃなくて、社会そのものを守る意味合いが強いんだよね
![半導体基板の図解とその上で動く機器群のイメージ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/048_semiconductor.png)
- 🦜 きなこ：半導体は世界中のデバイスの土台。そこにバグがあると、その上で動く全部の機器に影響するから、根っこの部分を守る感じなんだよね
- 🦜 きなこ：そう。だから狙われたら被害が大きいの。しかも今回はNATOとかENISAみたいな国際機関まで参加してるんだよね
![新規参加組織(Okta・Samsung・SK Hynix・SK Telecom)のロゴ群表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/051_new_members.png)
- 🦜 きなこ：顔ぶれで言うと、認証サービスのOktaや、半導体のSamsung・SK Hynix、通信キャリアのSK Telecomも新しく参加してるの

## Mythos Previewの能力進化と『守り』へのシフト

- 🦜 きなこ：白状するとね、この数字を最初に見たとき、私も思わず二度見しちゃったの
![OpenBSD 27年前のTCP SACKバグ発見のインパクト表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/062_old_bug.png)
- 🦜 きなこ：その前に、見つけたバグの中身がすごいの。OpenBSDに27年前から潜んでたバグまで、AIが自分で見つけちゃったんだよ
- 🦜 きなこ：そう。他にもFFmpegの16年前の欠陥や、FreeBSDの17年前のリモート攻撃可能なバグも見つけてるの
- 🦜 きなこ：前の世代のモデルは、攻撃コードを最後まで自力で組み立てる成功率が、ほぼ0%だったの
![エクスプロイトの定義を示す用語解説テロップ(英語表記: Exploit = code that abuses a vulnerability)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/068_exploit_def.png)
- 🦜 きなこ：厳密には違うの。エクスプロイトは、ソフトの欠陥を実際に突いて悪用するための攻撃コードのことだよ
![複数の小さなバグ(ガジェット)を繋ぎ合わせて一つの攻撃ルートを組み立てる図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/069_gadget_chain.png)
- 🦜 きなこ：しかも小さいバグを何個も繋いで、複数のパケットに分けて攻撃ルートを組み立てるくらい高度なこともやってのけるの

## 一般公開しない理由とASL-3安全装置

- 🦜 きなこ：いいところに気づいたね。実はそこがAnthropicにとっても一番の悩みどころなの
![非公開の理由を示すテロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/083_why_withheld.png)
- 🦜 きなこ：実はAnthropic自身が、まだ安全に一般公開できるレベルじゃないって、はっきり認めてるの
![「ASL-3(AI Safety Level 3)」の名称テロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/085_asl3_label.png)
- 🦜 きなこ：そのモヤッとする気持ち、実はちゃんと名前がついてるんだよ。『ASL-3』っていう安全基準なの
![Responsible Scaling Policy(RSP)全体とASL-3の位置づけ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/087_rsp_ladder.png)
- 🦜 きなこ：Anthropicの『Responsible Scaling Policy』っていう社内ルールの中で、一番厳しい保護基準の一つなの
- 🦜 きなこ：ううん。もともとは化学・生物兵器みたいな悪用や、モデルの中身が盗まれるのを防ぐための基準なの。サイバー能力もそこに含まれる形なんだよね
![「Detect and Block」多層防御の仕組み図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/090_detect_block.png)
- 🦜 きなこ：危険な出力をリアルタイムで検知して遮断する仕組みなの。専門的には『Detect and Block』って呼ばれてる

## GPT-5.4-Cyberとの戦略比較

![2026年4月のタイムラインテロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/102_timeline_2026.png)
- 🦜 きなこ：同時期の2026年4月に、OpenAIも独自のサイバー防衛モデルを発表してるの
![Anthropic(ゲートキーパー型) vs OpenAI(民主化型)の戦略比較表](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/103_strategy_compare.png)
- 🦜 きなこ：AnthropicのMythosは150組織だけに絞る『門番型』。OpenAIのGPT-5.4-Cyberは、数千人の専門家に開放する『民主化型』なの
- 🦜 きなこ：そこはしっかり本人確認をした上での話ね。あえて『拒否の境界線』を下げて、正当なセキュリティ業務には応じるよう調整されてるの
![SOCアナリストが監視画面を見ているイメージ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/109_soc_analyst.png)
- 🦜 きなこ：24時間体制で攻撃を監視するSOC、つまりセキュリティ運用センターのアナリストたちの作業を効率化する狙いがあるの
![OpenAI Preparedness Frameworkでの分類「High」の位置づけ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/111_preparedness_high.png)
- 🦜 きなこ：実はそこも違うの。OpenAIの安全評価だと、GPT-5.4-Cyberは『高』止まりで、最上位の『致命的』には届いてないんだよね
![攻撃側にAIが渡る前に防衛側へAIを届ける競争を時間軸で示す図解(英語表記: defense first race)](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/115_defense_race.png)
- 🦜 きなこ：まさにそれが両社共通の狙いなの。AI対AIの防衛競争は、もうこの瞬間から始まってるんだよね

## 導入コストと防衛側が直面する現実

- 🦜 きなこ：それだけ、防衛側が今すぐこの技術を使えるようにしたいっていう本気度の表れなんだよね
![利用料金(入力$25/出力$125・100万トークン当たり)の図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/120_pricing.png)
- 🦜 きなこ：実際すごい金額なんだよ。Mythos Previewの利用料、入力100万トークンあたり25ドル、出力は125ドルもするの
![一般的なAIモデルとMythos Previewの価格差イメージ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/122_price_gap.png)
- 🦜 きなこ：普通のチャットAIと比べると本当に別物の値段なの。それだけ計算資源を使ってるってことでもあるんだよね
- 🦜 きなこ：そうなの。だからAnthropicは、このプロジェクト全体で最大1億ドルの利用クレジットを用意して、負担を軽くしてるんだよね
- 🦜 きなこ：しかもオープンソースのセキュリティ団体には、別で400万ドルも直接寄付してるの
![AnthropicとOpenAIの助成金規模($1億 vs $1000万)の対比図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/126_grant_compare.png)
- 🦜 きなこ：OpenAIの方も1000万ドルの助成金プログラムを別で用意してる。両社とも単なる慈善じゃなくて戦略的な投資として動いてるの

## まとめ

![要点を対比で示すまとめスライド(図解内テキストは英語のみ: "Detection speed" vs "Remediation speed")](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/135_summary_contrast.png)
- 🦜 きなこ：今日のポイントをまとめると、AIが脆弱性を見つける速さが、人間が直す速さを追い越しちゃったってことなんだよね
- 🐹 もっちー：見つける力はもう化け物レベルやのに、直す方が追いつかへんっていうのがなんか皮肉やな
- 🦜 きなこ：150組織・15カ国・NATOも参加、10,000件超の脆弱性、41件中21件の攻撃成功…数字だけでも今日は盛りだくさんだったね
![門番型と民主化型、2つの戦略アイコンの再掲](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V200/139_two_strategies.png)
- 🦜 きなこ：150組織限定の『門番型』と、数千人に開く『民主化型』、どちらの戦略が主流になるかも、これから注目のポイントだね

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*