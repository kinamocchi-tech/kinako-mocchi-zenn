---
title: ChatGPTの記憶機能、実は覚えるだけじゃなかった｜人物像が自動で作られる【解説記事】
emoji: 🤖
type: tech
topics:
- chatgpt
- gdpr
- claude
- gemini
- ai
published: true
---

# ChatGPTの記憶機能、実は覚えるだけじゃなかった｜人物像が自動で作られる

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [ChatGPTの記憶機能、実は覚えるだけじゃなかった｜人物像が自動で作られる](https://www.youtube.com/watch?v=7oDq_kF8m3I)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、ChatGPTの記憶機能って、前に話したこと覚えといてくれるだけでしょ？
- 🐹 もっちー：人格まで！？そんなことできるようになったの？
- 🦜 きなこ：このDreaming V3がどう動いてて、なんで便利さと引き換えに新しいリスクを抱えてるのか、自分を守る方法まで含めて今日は全部見ていくね

## Dreaming V3の正体：2層構造の記憶

![同一チャット内では文脈を保持するが、チャットを閉じるとリセットされる従来の挙動を図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/012_visual_cue.png)
- 🦜 きなこ：でもそれ、そのチャットを閉じたら終わりなの。翌日に新しい会話を開いたら、また真っさらからやり直しだったんだよ
![2026年6月4日・米国Plus/Pro向け Dreaming V3 ロールアウト開始のタイムラインを表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/014_visual_cue.png)
- 🦜 きなこ：そこを根本から変えたのが、2026年6月4日に米国のPlusとProへ展開が始まったDreaming V3なんだよ
![2層構造の比較図（Reference Saved Memories と Reference Chat History）を表示し、上段を点灯](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/016_visual_cue.png)
- 🦜 きなこ：イメージは意外と近いの。ChatGPTの記憶はね、2つの層に分かれてる。1つ目がReference Saved Memories
![Saved Memories の管理画面イメージ（箇条書きリストとゴミ箱アイコン）を表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/018_visual_cue.png)
- 🦜 きなこ：「これ覚えといて」って自分から頼んだ事実のリストだよ。設定画面に一覧で並んでて、要らないものは自分で消せるの
![比較図の下段 Reference Chat History を点灯し、会話履歴からプロファイルが自動合成される矢印を表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/020_visual_cue.png)
- 🦜 きなこ：そう。もう1つがReference Chat History。過去の会話全体から、あなたがどんな人かを自動で合成し続ける層なの
![Diagram with two axes summarizing the design intent: 'Visible memory = transparency' and 'Invisible synthesis = convenience'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/022_visual_cue.png)
- 🦜 きなこ：そこがOpenAIの狙いなの。見える記憶で透明性を確保して、見えない合成で手間なしの便利さを取る。あえて2つに分けた設計なんだよ

## 展開の速さと精度の飛躍

- 🦜 きなこ：白状するとね、私、この機能が企業のアカウントに入るのはもっとずっと先だと思ってた。完全に読み違えたの
![Flow diagram: 'Early access 2 weeks' arrow leading to 'Default ON (unless admin opts out)'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/028_visual_cue.png)
- 🦜 きなこ：普通はそう。でも今回は約2週間の早期アクセス期間を挟んだあと、管理者がわざわざ切らない限りデフォルトでオンになる形なの
- 🦜 きなこ：そういうこと。裏を返せば、それくらいOpenAI側が性能に自信を持ってたってこと。実際、公式が出した数字の伸び方がすごいんだよ
![Before/Afterの棒グラフ。左「Recall 41.5%」灰色、右「82.8%」黄緑でぐっと伸びる](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/032_visual_cue.png)
- 🦜 きなこ：ユーザー個人の事実をちゃんと思い出せる割合が、41.5%から82.8%まで上がってるの。前提を毎回説明する手間が消えるレベル
![Second bar chart showing 'Time-aware update accuracy: 9.4% (2024) to 75.1% (2026)' side by side](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/034_visual_cue.png)
- 🦜 きなこ：近いね。もっと差が大きいのが、時間の経過を反映して記憶を書き換える精度で、9.4%から75.1%まで来てる
![タイムラインと2本のグラフが並んだ画面が、右下からゆっくり影に覆われていく](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/036_visual_cue.png)
- 🦜 きなこ：でしょ。だから企業もこの速さで飛びついた。ただね、その速さが別の問題も一緒に連れてきちゃったの

## 企業利用の落とし穴：プライバシーの矛盾

- 🦜 きなこ：そう思うよね。ところが実際は、そこが一番危ない思い込みなの。安心の根拠が、ひとつだけずれてるんだよ
![Center-screen comparison diagram: left panel 'Not used for training (Zero Data Retention)' with a checkmark, right panel 'Retained in memory (profile)' with a warning icon](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/039_visual_cue.png)
- 🦜 きなこ：『AIの学習に使わない』っていうポリシーと、会話を覚えていくメモリー機能は、そもそもまったく別のベクトルで動いてるの
![Left toggle labeled 'Training' is OFF and gray, right toggle labeled 'Memory' is ON and glowing, with a company document icon being pulled into a cloud on the right](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/041_visual_cue.png)
- 🦜 きなこ：そう。学習をオフに設定していても、メモリーがオンなら、会話の中身はプロファイルとしてクラウド上に残り続けるんだよ
![Admin console style UI with a highlighted badge reading 'Memory: ON by default', with a small note below reading 'Active until admin opts out'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/043_visual_cue.png)
- 🦜 きなこ：しかもEnterprise版は、管理者が明示的にオフにしない限りデフォルトでオン。誰も気づかないまま社内情報の合成が進むの
![From a panel labeled 'Retained in memory', three lines extend to industry icons (bank = finance, hospital = healthcare, scale = legal); the finance icon lights up red first](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/045_visual_cue.png)
- 🦜 きなこ：金融がまさにそう。SECとFINRAっていう規制当局の、すごく厳しい記録保持ルールに従わないといけない業界なの
- 🦜 きなこ：でも記憶された内容を完全に監査したり、決められた期間で破棄したりが制御できない。だから契約なしの利用は違反になりかねないと指摘されているの

## 忘れる権利と『焼き上がったケーキ』の壁

![同意チェックボックスが空欄のまま、裏側でユーザープロファイルが自動生成されていく対比図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/056_visual_cue.png)
- 🦜 きなこ：そう。しかもGDPRは「明示的で曖昧さのない同意」を求めるの。黙って人物像を作られるのは、そこに引っかかりやすいんだよ
- 🦜 きなこ：そこが緊張関係なの。実際、プライバシー規制の影響でEU圏では展開に制限が出てるって指摘もあるんだよ
![左：表の一行を削除するDBの図／右：ベクトル空間全体に影響が広がって消せないAI記憶の対比図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/060_visual_cue.png)
- 🦜 きなこ：それがね、AIの記憶はデータベースの一行みたいに独立してないの。学習した影響がモデル全体に溶け込んでるんだよ
![焼き上がったケーキの断面に青い着色料が全体へ拡散している図と、ピンセットで一滴だけ抜こうとして✕印がつくイラスト](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/061_visual_cue.png)
- 🦜 きなこ：たとえるなら、もう焼き上がったケーキの中から、青い着色料を一滴だけ抜き取るようなものなの
![Title card reading 'Machine Unlearning', connected by lines to a cake-and-dye icon and a 'right to be forgotten' icon](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/064_visual_cue.png)
- 🦜 きなこ：そういうこと。その「特定のデータの影響だけを取り除く技術」をMachine Unlearning、機械の忘却って呼ぶんだよ
![A deep gap between 'Right to be Forgotten' and 'AI Memory', with a warning icon indicating an unresolved challenge](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/065_visual_cue.png)
- 🦜 きなこ：性能を落とさずにそれをやるのは、今のAIの構造では極めて難しい未解決課題なの。忘れる権利との溝は、まだ埋まってないんだよ

## ライバルはどう違う？ Claude・Geminiとの設計思想比較

![OpenAI・Anthropic・Googleの3社ロゴが横並びになり、その下に空の比較表が現れる](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/067_visual_cue.png)
- 🦜 きなこ：いい疑問だね。実は3社とも記憶の作り方が全然違うんだよ。同じ『覚える』でも、設計の思想からして別物なの
![Comparison table, OpenAI column filled in with 'Automatic profile synthesis / boundary is the whole account'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/069_visual_cue.png)
- 🦜 きなこ：じゃあ友達に例えるね。ChatGPTは何でも勝手にメモして、どの話題にもそのメモを持ち込んでくる友達なの
![Comparison table, Anthropic column filled in with 'Strict isolation per project', with a notebook splitting into three separate notebooks](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/071_visual_cue.png)
- 🦜 きなこ：そう。それに対してClaudeは、話題ごとにノートをきっちり分けて置いておく几帳面な友達なんだよ
![「Projects」と書かれた箱の中に指示書と資料が閉じ込められ、外側へ伸びる矢印が×印で遮られる図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/072_visual_cue.png)
- 🦜 きなこ：Projectsって機能で、そのノートの中身は外に漏れないの。仕事の話は仕事のノートの中だけ
![24時間の時計アイコンから1枚のサマリー文書が生成され、ユーザーが編集ペンを持つ図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/074_visual_cue.png)
- 🦜 きなこ：しかも会話のたびに要点をまとめ直して、その要約を自分で全部読んで、書き換えることもできるの
![Comparison table, Google column filled in with 'Linked to Search/Gmail/Drive / boundary is the workspace', completing the three-company table](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/077_visual_cue.png)
- 🦜 きなこ：検索履歴やGmailまで繋がって、生活まるごとを文脈にするの。便利だけど、預ける情報は一番多いんだよ

## 見えないリスク：思想の偏向とMCP経由の流出

- 🦜 きなこ：その感覚、すごく大事なんだよ。実はさっき話してた自動合成、まさにそこが暴走する怖さなの
![色とりどりの点群が、矢印の先で1色のベタ塗りブロックに圧縮される図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/081_visual_cue.png)
- 🦜 きなこ：心理学に『カラーメモリ』って現象があってね。人の記憶って正確な事実じゃなくて、典型的な型にどんどん単純化されていくんだよ
- 🦜 きなこ：そう、それ。もっちーのたとえ、今日いちばん的確だよ。同じ圧縮が、AIのプロファイル合成の中でも起きちゃうの
![Diverse opinion speech bubbles (left-leaning, right-leaning, neutral) pass through a funnel and converge into a single generic label](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/084_visual_cue.png)
- 🦜 きなこ：たとえば研究目的でいろんな思想の話題を調べただけなのに、AIが『この人はこういう立場の人』って一つのラベルに圧縮しちゃう
![ユーザーを包む泡の内側に、AIが内側から追加でラベルを貼り足していく図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/086_visual_cue.png)
- 🦜 きなこ：近いね。でも違うのは、偏らせてるのが自分のクリックじゃなくてAI側の要約ってこと。AIが勝手にフィルターバブルを作っちゃうの
- 🦜 きなこ：怖いのは覚えられることそのものじゃなくて、雑に決めつけられて要約されることなんだよ

## 自分を守る実践Tips

![Header card reading 'Deleting memory: 4 steps + Temporary Chat', with a flow diagram: Settings to Personalization to Memory to Delete](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/095_visual_cue.png)
- 🦜 きなこ：大丈夫だよ、もっちー。誤って覚えられた記憶は、自分の手でちゃんと消せるようになってるの
![STEP1/4 の操作フロー図。ChatGPT 画面の左下プロフィールアイコンを黄色い矩形でハイライトし、展開メニューの「Settings」に赤い矢印](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/097_visual_cue.png)
- 🦜 きなこ：まずは画面左下のプロフィールアイコンをクリックして、開いたメニューからSettingsを選ぶんだよ
![STEP2/4 の操作フロー図。設定画面左サイドバーの「Personalization」タブを矩形ハイライトし、右ペインの「Memory」セクションまで下向きスクロール矢印を表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/098_visual_cue.png)
- 🦜 きなこ：次に左の設定メニューからPersonalizationタブを開いて、Memoryのところまでスクロールするの
![STEP3/4。「Manage memories」ボタンを矩形ハイライトし、クリック後に開く記憶リストのモーダル（箇条書きの事実が並ぶ画面）を並べて表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/100_visual_cue.png)
- 🦜 きなこ：そこにManage memoriesってボタンがあるの。押すと、AIが覚えてる事実の一覧がずらっと出てくるよ
![STEP 4/4. A memory list row reading 'Works in the healthcare industry' is boxed in red, with a cursor clicking the trash icon on the right and a callout indicating deletion of just this one entry](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/102_visual_cue.png)
- 🦜 きなこ：それが例の暴走ね。その行の右にあるゴミ箱アイコンを押せば、その一件だけを個別に削除できるの
![Alternative route card. Chat input box showing the typed text 'Forget that I work in the healthcare industry', with a caption below reading 'Shortcut to delete without opening settings'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/104_visual_cue.png)
- 🦜 きなこ：しかもチャット欄にForget that I work in the healthcare industryって打つだけでも消せるんだよ

## まとめ

![Center-screen card titled 'Today's Summary' with a heading and a 3-item checklist fading in](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/109_visual_cue.png)
- 🦜 きなこ：じゃ、今日のまとめいくね。AIの自動記憶は、便利さと引き換えに新しい管理責任が生まれる、っていうのが今日の話だったの
- 🐹 もっちー：最初は勝手に覚えてくれて楽だな、くらいにしか思ってなかったけど、まさかここまで奥が深い話だったとはな
![Summary card with three icons lighting up side by side: 'Where it's stored / Who can see it / How to delete it'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/111_visual_cue.png)
- 🦜 きなこ：どこに保存されて、誰が読めて、いつ消せるのか。この三つさえ押さえておけば、必要以上に怖がらずに使いこなせるんだよ
![A large card titled 'Save this checklist' condensing the setup steps into one image](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V211/112_visual_cue.png)
- 🐹 もっちー：で、さっきの設定の手順な！画面開いて順番にポチポチするだけやったやろ。よし、あれ保存しとこ！

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*