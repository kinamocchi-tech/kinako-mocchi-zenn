---
title: 輸出規制で止まったAIを18日で復活させた3手｜Claude Fable 5【解説記事】
emoji: 🤖
type: tech
topics:
- voicevox
- ai
- claude
- llm
- tech
published: true
---

# 輸出規制で止まったAIを18日で復活させた3手｜Claude Fable 5

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [輸出規制で止まったAIを18日で復活させた3手｜Claude Fable 5](https://www.youtube.com/watch?v=prOh3N_9KFY)
:::

## この記事で分かること

- 🐹 もっちー：国から止められることってあるんだ？もうそのAI、二度と戻ってこないんじゃないの？
- 🦜 きなこ：そう、そこが今日の話。政府と何を交渉して、AI自身の何を変えたことで許可が下りたのか——その中身を順番に見ていくね
- 🐹 もっちー：そういえば、さっき言ってたMythos 5ってやつも、Fable 5と一緒に戻ってきたの？
- 🦜 きなこ：うん。しかもね、Anthropicが動いたのは政府との交渉だけじゃないの。それも含めて見ていこうね

## 何が起きたのか（輸出規制の内容）

![「Remote access = Export」EAR §734.13（リモートアクセスを輸出とみなす規定）の図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/016_cue.png)
- 🦜 きなこ：そこ、いい引っかかり方なんだよ。今回はね、ネット越しにAIを使わせること自体を「輸出」とみなす、っていう解釈が使われたの
![2026年6月12日 米商務省BIS → Anthropic へレター送付。対象モデル: Claude Fable 5 / Mythos 5](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/018_cue.png)
- 🦜 きなこ：2026年6月12日、アメリカ商務省のBISって部署が、Fable 5とMythos 5を名指ししたレターをAnthropicに送ったの
![レターの要求内容: 外国籍者のアクセスには承認済み輸出ライセンスが必要（Anthropicの外国籍従業員も対象）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/020_cue.png)
- 🦜 きなこ：そう、産業安全保障局。レターが求めたのは、外国籍の人がこの2つに触るなら承認済みの輸出ライセンスを取れ、ってこと
![対象範囲: 特定国の指定なし →「Any foreign national」＝事実上の全世界。自社の外国籍従業員も含む](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/022_cue.png)
- 🦜 きなこ：それが、特定の国は一つも出てこないの。対象は「あらゆる外国籍者」。Anthropicで働く外国籍の社員まで含まれてた
- 🦜 きなこ：そう。しかもね、Anthropicには使ってる人がどこの国籍かを確かめる手段がないの
![6月12日 午後5時21分（米東部時間）指令受領 → 全顧客向けに Fable 5・Mythos 5 を無効化](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/026_cue.png)
- 🦜 きなこ：そういうこと。だから6月12日の午後5時21分、米東部時間ね。Anthropicは全顧客向けに、この2つのモデルを止めたの

## 引き金になった出来事

- 🦜 きなこ：実はね、あの停止には、はっきりした引き金になった出来事があるの。しかもそれ、Anthropic自身が公表してることなんだよ
![「Amazon researcher's jailbreak report → BIS export control」という因果フロー図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/032_cue.png)
- 🦜 きなこ：Amazonのリサーチャーが、Fable 5のサイバーセキュリティの安全装置を破ったっていう報告。これが規制の引き金なの
![用語テロップ「Jailbreak = bypassing AI safeguards with words」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/034_cue.png)
- 🦜 きなこ：ハッキングとはちょっと違うの。ジェイルブレイク——AIに組み込まれた安全装置を、言葉の工夫でするりと迂回させる手口のことなんだよ
![「Bypass safeguard」→「Identify vulnerability」の2段ステップ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/036_cue.png)
- 🦜 きなこ：近いね。しかもそのリサーチャーは、迂回した先でFable 5に、実際のソフトの弱点まで特定させたって報告されてる
![「Vulnerability found」から「Exploit code generated」まで進んだ事例を示す段階図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/038_cue.png)
- 🦜 きなこ：ある事例では、その弱点を突く攻撃コードそのものまで書かせたって報告されてる。穴を見つけて、攻め方まで出させたの
![対比パネルの左側「Admin's concern: consumer product → unrestricted cyber tool」を表示（右側は空欄のまま）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/040_cue.png)
- 🦜 きなこ：そこなの。政権側はこれを、消費者向けの製品が、そのまま無制限のサイバーツールに変わってしまうリスクだと受け取ったんだよ

## 2週間の交渉

- 🦜 きなこ：「たった18日で戻ってきた」って引っかかったの、すごく正しいと思う。私も最初、そこが一番の謎だったの
![発言者カード: 米商務長官 Howard Lutnick（ハワード・ラトニック）／日付ラベル「June 30, 2026」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/049_cue.png)
- 🦜 きなこ：動きはちゃんとあったんだよ。アメリカの商務長官、ハワード・ラトニックが6月30日にこう言ってるの
![引用カード: 「Over the past two weeks, we have worked closely with Anthropic to analyze and approve Fable 5」＋下段に和訳を併記](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/050_cue.png)
- 🦜 きなこ：「過去2週間、我々はAnthropicと緊密に作業して、Fable 5を分析し、承認した」って投稿してるの
![交渉当事者カード: 規制発出=BIS（産業安全保障局）／米政府側=Howard Lutnick 商務長官／Anthropic側=Dario Amodei CEO](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/052_cue.png)
- 🦜 きなこ：規制を出したのはBIS、産業安全保障局。でも表に名前が出るのは、政府側がラトニック商務長官、Anthropic側がダリオ・アモデイCEO
![同カードに注記追加: 「Specific team/dept unconfirmed」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/054_cue.png)
- 🦜 きなこ：そこは正直に言っておくね。この二人以外の交渉チームや担当部署の名前は、一次ソースでは特定できなかったの
![合意3条件リスト 1/3 点灯: 「Proactively detect and address security risks」](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/056_cue.png)
- 🦜 きなこ：合意した条件は三つあるの。一つ目は、セキュリティのリスクを自分から能動的に検知して、対処していくこと

## 新しい安全性分類器という技術対応

![「Negotiation」と「Technical fix」を2本柱で並べた対比テロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/065_cue.png)
- 🦜 きなこ：いい疑問だね。だからAnthropicは、政府との約束だけで終わらせないで、AIの中身そのものにも同時に手を入れてるの
![「Defense in depth」テロップ＋壁を何枚も重ねた断面イラスト](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/067_cue.png)
- 🦜 きなこ：まず考え方の話ね。守りを一枚の壁で済ませないで、何枚も重ねて置く。これを多層防御って呼ぶんだよ
![「Blocks 99%+ of reported methods」の数字強調カード](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/069_cue.png)
- 🦜 きなこ：そう。その重ねた守りで、今回報告されたジェイルブレイクの手口は、99パーセントを超えるケースで止められるようになったの
![「99% = rate for this specific method only」と限定条件を添えた注釈カード](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/071_cue.png)
- 🦜 きなこ：そこは正確に言うね。あれは報告されたあの手口に対しての数字なの。どんな攻撃にも効く万能の合格点じゃないんだよ
- 🦜 きなこ：それとね、もう一つ。サイバー攻撃まわりの用途を見分ける専用の分類器も、まるごと新しいものに入れ替えたの
![4層分類カードを1層ずつ順に表示（禁止／高リスク・デュアルユース／低リスク・デュアルユース／無害）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/075_cue.png)
- 🦜 きなこ：聞かれた用途を4つの層に仕分けるの。禁止、高リスク、低リスク、無害。層ごとに答え方を変える作りなんだよ

## 競合を含む業界横断の枠組みづくり

![Anthropic・Amazon・Microsoft・Google＋Glasswingパートナーの企業名カードを横並びで表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/082_cue.png)
- 🦜 きなこ：そう、そこが今回いちばん異例なところ。Amazon、Microsoft、Googleと、Glasswingのパートナーと組んで起草してるの
![壁が横に4枚並び、1枚だけ穴を塞いでも隣の壁が空いたままの図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/084_cue.png)
- 🦜 きなこ：組んでるのは弱点の告白じゃなくて、ものさしの共有なの。1社で自分の穴を塞いでも、隣が空いたままなら意味がないよね
![4基準リストカード（1 能力獲得／2 能力獲得の広がり／3 武器化の容易さ／4 発見可能性）を縦に並べて表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/086_cue.png)
- 🦜 きなこ：そうなの。だからジェイルブレイクの深刻さを4つの基準で採点する案を作ってる。能力獲得、その広がり、武器化の容易さ、発見可能性
![4基準リストの右側に空欄の評価列を足した当てはめ表（見出し: Amazonリサーチャーの事例）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/088_cue.png)
- 🦜 きなこ：じゃあ、前に話したAmazonのリサーチャーの件を当てはめてみるね。Fable 5に脆弱性を見つけさせた、あの一件
![当てはめ表の『Capability gain = small』『Breadth = limited』の2行がハイライト表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/090_cue.png)
- 🦜 きなこ：まず能力獲得は小さい。見つかったのは既知で軽微な脆弱性で、新しい力を与えたわけじゃないから。広がりも限定的なの
![当てはめ表の『Ease of weaponization = high』『Discoverability = high』の2行が追加ハイライトされ4行が揃う](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/092_cue.png)
- 🦜 きなこ：ところが武器化の容易さは高め。攻撃コードをそのまま作らせた事例まで報告されてるからね。しかも発見可能性も高いの

## この一件が示すAIガバナンスの実務

![『Restriction』→『Technical fix + govt deal』→『Lifted』の因果図の1コマ目。左端に赤い『Restriction』カードだけが表示された状態](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/099_cue.png)
- 🦜 きなこ：終わったのは今回の一件だけ。でも大事なのは、その解き方の型が残ったことなの。一度止まったら終わり、じゃないって実例で示されたんだよ
![因果図の2〜3コマ目。『Technical fix + govt deal』が矢印でつながり、右端に『Lifted (day 18)』が現れて3コマが完成する](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/100_cue.png)
- 🦜 きなこ：規制がかかる、技術で危険を潰して政府と合意する、そして解除される。この三手を18日でやり切った実績が残ったの
- 🦜 きなこ：そういうこと。しかもこの一件は、もう一つ別の意味でも先例として注目されてるの。AIの規制を考える政策の専門家のあいだでね
![『Remote access (API use) = Export』を示す図解。国境をまたぐ矢印がモノではなくデータで描かれ、EAR §734.13 の条番号を添える](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/103_cue.png)
- 🦜 きなこ：アメリカは、API越しにモデルを使わせることまで『輸出』とみなしたの。EARの734.13条、リモートアクセスの規定を当てはめてね
![ECRA新興技術規制・EAR §744.22・§734.13 といった条文名が次々に積み上がる細かい注釈カード（情報過多を演出）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/105_cue.png)
- 🦜 きなこ：そうなの。CSISの分析だと、ECRAの新興技術規制を使った点も注目されててね。しかも根拠のレターは非公開だから、条文の特定まで分析頼みで——
- 🦜 きなこ：……あ、ごめん。つい細かいところが楽しくなっちゃって。話を戻すね

## まとめ

![3本柱（技術対応・政府合意・業界連携）を1枚に並べたクロージングカード](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V250/111_cue.png)
- 🦜 きなこ：今日の話、まとめるね。一度止められたAIが、技術対応と政府合意、それに業界連携の3本柱で18日で戻ってきたの
- 🐹 もっちー：AIも国と話し合いするんだね。ぼくも回し車止められたとき、飼い主とちゃんと話し合って再開してもらったことあるよ
- 🦜 きなこ：そのたとえ、案外近いかもね。止められて終わりじゃなくて、話し合って戻ってくる、っていう流れが一緒だから
- 🐹 もっちー：AIの世界も、意外と話し合いで解決できることが多いんだな。ちょっと安心したよ

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*