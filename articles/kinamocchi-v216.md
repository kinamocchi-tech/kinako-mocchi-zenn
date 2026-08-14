---
title: Apple公式にGeminiの文字が無い謎｜WWDC2026で本当に変わったのはSiriじゃない【解説記事】
emoji: 🤖
type: tech
topics:
- apple
- siri
- gemini
- wwdc2026
- ai
published: true
---

# Apple公式にGeminiの文字が無い謎｜WWDC2026で本当に変わったのはSiriじゃない

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [Apple公式にGeminiの文字が無い謎｜WWDC2026で本当に変わったのはSiriじゃない](https://www.youtube.com/watch?v=g0VH4kZtjNg)
:::

## この記事で分かること

- 🐹 もっちー：新しいSiri、中身はGoogleのGeminiに置き換わったんやろ？ニュースで散々見たで！
- 🐹 もっちー：え、一文字も？あんなに話題になってたのに？
- 🐹 もっちー：じゃあ報道のほうが嘘ついてたってこと？
- 🐹 もっちー：なんでそんな回りくどい出し方するの…？

## WWDC 2026 で Apple が発表したもの

- 🦜 きなこ：そこなんだよ。発表そのものは公式にちゃんとあるの。しかも中身はかなり具体的なんだよ
![WWDC 2026 のタイトルカード風図解（開催日 2026年6月8〜9日／発表名『Siri AI』を大書き）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/018_cue.png)
- 🦜 きなこ：WWDC2026、6月8日と9日。そこでAppleが出したのがSiri AIっていう新しいSiriなの
![旧 Siri と Siri AI の位置づけ比較図（機能追加ではなく作り直しであることを矢印で対比）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/020_cue.png)
- 🦜 きなこ：違いは規模なんだよ。一部を改良したんじゃなくて、Siriをまるごと作り直したフルリビルド版なの
![対応デバイス5種のアイコン展開図（iPhone / iPad / Mac / Apple Watch / Apple Vision Pro）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/022_cue.png)
- 🦜 きなこ：別物。しかもiPhone、iPad、Mac、Apple Watch、Apple Vision Proに深く統合されるって書いてあるの
![既存アプリ横断＋独立したスタンドアロンアプリの2階建て構成図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/024_cue.png)
- 🦜 きなこ：それにね、今までどおりアプリをまたいで動くのに加えて、Siri専用の新しいアプリとしても出てくるの
![会話履歴が iCloud 経由で iPhone / iPad / Mac に同期されるイメージ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/026_cue.png)
- 🦜 きなこ：前に聞いたことを開いて見返せるの。会話の履歴はiCloudで端末どうし同期されるんだよ

## 「Siri＝Gemini」は正しいのか — 提携の実体

- 🦜 きなこ：そう思うよね。私も見出しだけ追ってた頃は、まったく同じように読んでたの
- 🦜 きなこ：共同声明の原文はね、書き方がちょっと違うの
![共同声明の引用テロップ。図中テキストは英語で『built on Google's Gemini models and cloud technology — Joint statement, Jan 12, 2026』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/039_cue.png)
- 🦜 きなこ：今年1月12日に出た文には、次世代の Apple Foundation Models は Gemini のモデルとクラウド技術で構築される、って書いてあるの
![2枚並置の対比図。図中テキストは英語で左『Who taught the model』右『Who answers at runtime』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/042_cue.png)
- 🦜 きなこ：そう、そこが別の話なの。作るときに手を借りたのかと、いま喋ってる本人が誰なのかはね
![報道ベースであることを示す注記カード。図中テキストは英語で『Report: shipped models contain no Gemini weights — AppleInsider (not officially confirmed)』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/045_cue.png)
- 🦜 きなこ：報道の検証記事では、出荷されるモデルに Gemini の重みは一滴も入っていないと伝えられてる
- 🦜 きなこ：あくまで報道ベースだけど、Gemini は教師役、いわゆる蒸留に使われたとみられてるの

## Google のサーバーで動くのにプライバシーは守れるのか — PCC の外部拡張

- 🦜 きなこ：白状するとね、私も最初は『それってもうAppleのプライバシーじゃないよね』って思ってたの
![Apple データセンター → Google Cloud への PCC 拡張マップを表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/061_cue.png)
- 🦜 きなこ：Appleはセキュリティブログで、Private Cloud Computeを初めて自社のデータセンターの外に出したって発表したの
![Apple Intelligence のワークロードが Google Cloud（NVIDIA GPU）へ流れる構成図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/063_cue.png)
- 🦜 きなこ：GoogleのクラウドとNVIDIAのGPUの上。両社と協働して、新しいApple Intelligenceの処理を動かすんだよ
- 🦜 きなこ：私もそこで身構えたの。でもAppleが言ってるのは『場所は借りるけど、保証ごと持っていく』ってことなんだよ
![PCC の保証①ステートレス計算を積み上げ表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/066_cue.png)
- 🦜 きなこ：保証は3つ。1つ目がステートレス計算。処理が終わったら、ユーザーのデータを一切残さないの
![PCC の保証②非ターゲット可能性を積み上げ表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/068_cue.png)
- 🦜 きなこ：2つ目が非ターゲット可能性。特定の誰か一人を狙い撃ちして処理を覗くことができない設計なの

## 本当の主役 — 誰の AI でも差し替えられる仕組み

- 🦜 きなこ：そう思うよね。じゃあ想像してみて。もっちーがいつも使ってるアプリ、中身は一行も書き直してないの
![アプリの外箱はそのまま、中のAIブロックだけが別会社のものに差し替わるアニメーション図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/084_cue.png)
- 🦜 きなこ：なのに、その中で動いてるAIだけが、別の会社のものに入れ替わってるの
- 🦜 きなこ：そう。しかも入れ替える相手は開発者が選べるの。Apple製でも、よその会社のでもいい
![見出しテロップを中央に大きく提示する。図中テキストは英語で『Model abstraction layer』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/088_cue.png)
- 🦜 きなこ：今まではそうだったの。これね、モデル抽象化レイヤーっていう名前がついてるんだよ
![壁の差し込み口（ソケット）とプラグの比喩イラスト。形が同じなら誰のプラグでも挿さることを示す](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/090_cue.png)
- 🦜 きなこ：大丈夫。差し込み口の形を一種類に決めた、って思ってくれたらいいよ
![API 名テロップ。図中テキストは英語で『LanguageModel protocol』、出典ラベルは『WWDC26 Session 241』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/092_cue.png)
- 🦜 きなこ：その例え、いいね。その差し込み口が LanguageModel っていうプロトコルなの

## 「iOS 27 Extensions」は存在するのか — 通念の答え合わせ

![左右2列の対比表。図中テキストは英語で左『As reported』右『Confirmed by Apple』。左列に『iOS 27 Extensions』を置き、右列は空欄のままにする](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/108_cue.png)
- 🦜 きなこ：それがね、私が確認できたApple公式のページには、その名前がひとつも出てこないの
![取り消し線付きの語と正しい言い換えを並べたテロップ。図中テキストは英語で、赤の取り消し線に『Does not exist』、緑に『Not confirmed in this primary source』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/112_cue.png)
- 🦜 きなこ：そこは慎重にいこう。「無い」じゃなくて「この一次ソースでは確認できない」が正確な言い方なの
- 🦜 きなこ：全然違うよ。私が見ていないページに載ってる可能性は残るからね。だから私は断言しないの
![対比表の右側に LanguageModel プロトコルを緑文字で追加表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/116_cue.png)
- 🦜 きなこ：公式で確認できたのはLanguageModelプロトコル。他社のAIに差し替える入口は、こっちなんだよ
![対比表の1項目に黄色のラベルを貼る。図中テキストは英語で項目名『AI Extensions marketplace』、ラベル『Unverified』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/118_cue.png)
- 🦜 きなこ：掲載条件も審査基準も収益分配も、公式では確認できないの。あるとも無いとも言えない、宙ぶらりんの状態
![用語リストに［要確認］ラベル: iOS 27 Extensions / PCC 2.0 / Gemini for Apple Intelligence](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/120_cue.png)
- 🦜 きなこ：「PCC 2.0」も「Gemini for Apple Intelligence」も同じ。公式のブランド名としては確認できないの

## Apple は AI 競争に負けたのか — 未確定のまま残るもの

- 🦜 きなこ：そう受け取るの、すごく自然だと思う。実際そう論じてる書き手もいるし、その気持ちは分かるの
![Forbes 寄稿記事の見出しを引用した図。赤いラベルを大きく添え、図中テキストは英語で見出し『Apple's AI surrender』、ラベル『Opinion』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/131_cue.png)
- 🦜 きなこ：Forbesの寄稿欄は、見出しがそのまま『AppleのAI降伏』。戦略的降伏って書いてるブログもあるの
- 🦜 きなこ：でもそれ、論説なの。書いた人の読み方であって、確かめられた事実じゃないんだよ
![3レーンの分類図。図中テキストは英語で『Confirmed』『Reported』『Unverified』。Unverified レーンの1枚目のカード（英語で『Contract term and total value』）が点灯する](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/135_cue.png)
- 🦜 きなこ：大きく三つ。まず契約がマルチイヤーとしか出てなくて、正確な期間も総額も分からないの
![Unverified レーンの2枚目のカードが点灯。図中テキストは英語で『Existing ChatGPT integration』と3分岐『Continue』『End』『Coexist』を示し、いずれも確定していないことを示す](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/136_cue.png)
- 🦜 きなこ：二つめ。今のiPhoneに入ってるChatGPT連携が、新しいOSでどうなるか誰も答えてないの
![未確認レーンの3つめのカードが点灯。推論時のルーティング（端末内／PCC 経由）に大きな『?』を重ねた図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/137_cue.png)
- 🦜 きなこ：三つめ。実際に売られる端末が、答えを出すときどこまでGeminiを動かすのか。ここも未確認

## まとめ

- 🐹 もっちー：ぼく最初、Siri の中身がまるごと Gemini になったって思い込んでた
- 🦜 きなこ：そう思うよね。提携は本当。でも Gemini は主に学習の先生として使われたって伝えられてる
- 🐹 もっちー：じゃあ公式に Gemini の文字が無かったのも、隠してたわけじゃないんだ
![冒頭の謎の回収図。Apple 公式ページと自社セキュリティブログを並べ、図中テキストは英語で『Consumer page: no partner named』『Security blog: partner disclosed』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V216/150_cue.png)
- 🦜 きなこ：Apple はコンシューマー向けの発表で、クラウドの相手を名指ししないの

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*