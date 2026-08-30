---
title: Claude Opus 5の30.2%、信じていい数字はどっち？ARC-AGI-3の衝撃
emoji: 🤖
type: tech
topics:
- arc-agi-3
- agi
- frontier-bench
- ai
- llm
published: true
---

<!-- グラレコ:graphreco -->
![Claude Opus 5の30.2%、信じていい数字はどっち？ARC-AGI-3の衝撃【解説記事】｜グラレコ要約](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/V270_graphreco.png)

# Claude Opus 5の30.2%、信じていい数字はどっち？ARC-AGI-3の衝撃

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [Claude Opus 5の30.2%、信じていい数字はどっち？ARC-AGI-3の衝撃](https://www.youtube.com/watch?v=YCj5mElN7MA)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、人間なら100点取れるのに、AIだと1点も取れないテストがあるって知ってた？
- 🐹 もっちー：1%未満って、ほぼゼロってことじゃん。何それ、そんなに難しいの？
![対比バーグラフ。図中テキストは英語で『ARC-AGI-3 score: under 1% → 30.2%』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/005_bar_score_jump.png)
- 🐹 もっちー：30.2%！？ ほぼゼロやったのが、いきなり30かい！
- 🐹 もっちー：値上げしてないの？ そこは普通、上げるところでしょ…

## 「3倍」の正体 — 30.2%と7.8%

![ARC Prize 公式結果ページのスクリーンショット風図解（『Claude Opus 5 (High) is the highest-performing model on ARC-AGI-3』の引用を強調）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/014_arc_prize_quote.png)
- 🦜 きなこ：まず30.2%から。この数字ね、Anthropicが自分で言ってるんじゃないの
- 🦜 きなこ：テストを作って運営してる側。ARC Prizeっていう団体が、公式の結果ページで最高性能だって認定してるの
- 🦜 きなこ：そこが大事なの。作った人が測ると、宣伝じゃなくて記録になるんだよ
![30.2% と 7.8% の対比バーグラフ。Opus 5 と GPT-5.6 Sol のラベル付き](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/020_bar_30_vs_8.png)
- 🦜 きなこ：それまでの最高がGPT-5.6 Solで7.8%。Anthropicの発表文には、次点モデルの3倍って書いてあるよ
![計算テロップ。図中テキストは英語で『30.2 ÷ 7.8 = about 3.87x』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/022_calc_multiplier.png)
- 🦜 きなこ：そう思うよね。でも割ってみて。30.2を7.8で割ると、約3.87倍なの
![設定の注記カード。図中テキストは英語で『High effort — raw 30.16%, reported 30.2%』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/024_effort_setting_note.png)
- 🦜 きなこ：Highっていう、いちばん深く考えさせる設定で走らせたときの点数なの。生の値は30.16%で、それを丸めて30.2%だよ

## 人間100%・AI1%未満のテスト

![説明書のない見知らぬゲーム画面のイラスト。プレイヤーが目的不明のまま操作している構図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/033_mystery_game_screen.png)
- 🦜 きなこ：もっちー、想像してみて。知らないゲームの画面を渡されるの。説明書なし、チュートリアルなし
- 🦜 きなこ：教えてくれない。ゴールが何かも言われないの
![4枚のカードが順に点灯する図。図中テキストは英語で『1. Explore』『2. Infer the goal』『3. Build a world model』『4. Learn continuously』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/040_four_step_cards.png)
- 🦜 きなこ：それがARC-AGI-3が測ってる能力そのものなの。未知の環境を探索して、その場でゴールを推測して、頭の中に世界のモデルを作って、続けて学ぶ。この4つ
![左側の観察メモと右側の4要素カードを線で結んだ対応図（キャラクターは描かない）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/042_notes_to_cards_map.png)
- 🦜 きなこ：そう。点が入ったやり方を覚えとくって言ったでしょ。あれが継続学習だよ
- 🦜 きなこ：人間は全員それができるの。だからテスト受験者は全部の環境を解けたんだよ
![禁止マーク付きテロップ。図中テキストは英語で『No natural-language instructions』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/045_no_instructions_ban.png)
- 🦜 きなこ：しかもこのテスト、言葉での指示を一切くれないの。自然言語のヒントなしで、動いて確かめるしかない

## 静的パズルから対話型へ — 設計思想の転換

![ARC-AGI-1 → ARC-AGI-2 → ARC-AGI-3 の年表風タイムライン](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/053_timeline_arc_versions.png)
- 🦜 きなこ：ARC-AGIって、実は3代目なの。1と2があって、そこから作りが変わったんだよ
![ARC-AGI-1/2 の静的な図形パズル例（入力グリッドと出力グリッドが並んだ形式）の図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/055_static_grid_puzzle.png)
- 🦜 きなこ：図形のパズルなの。問題が目の前に全部並んでて、規則を見つけて答えを出す。じっと見て考えるタイプだね
![ARC-AGI-3 の対話型ループ図（行動 → 環境の反応 → 学習 → 次の行動）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/057_interactive_loop_diagram.png)
- 🦜 きなこ：3は用紙がないの。自分で動いて、返ってきた反応を見て、また動く。ターン制なんだよ
- 🦜 きなこ：そのたとえ、すごくいいよ。しかも森には案内板がひとつもないの
![転換を示す矢印図。図中テキストは英語で『Test of what you already know』から『Test of what you can learn from scratch』へ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/061_test_paradigm_shift.png)
- 🦜 きなこ：パズルだとね、たくさん見て覚えたモデルが強くなっちゃうの。知ってるかどうかのテストになりやすいんだよ
- 🦜 きなこ：測りたかったのは、初めての場所でその場から学べるかどうか。だから中で動けるテストに作り直したの

## 誰も解けなかった5つの環境と「新規行動」

![見出しテロップ。図中テキストは英語で『5 environments no model had beaten — cleared 100%』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/073_five_envs_headline.png)
- 🦜 きなこ：Opus 5はね、それまでどのモデルも突破できてなかった環境を5つ、追加で全部クリアしたの
![突破された5環境の名前カード（ar25 / ft09 / lp85 / r11l / s5i5）を並べて表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/075_five_env_names.png)
- 🦜 きなこ：エーアール25、エフティー09、エルピー85、アールイレブンエル、エスファイブアイファイブ。記号みたいな名前だよ
![引用カード。図中テキストは英語で『novel behavior』とし、出典ラベルは『ARC Prize』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/076_novel_behavior_quote1.png)
- 🦜 きなこ：でね、ARC Prizeはその様子を新規行動、英語でノベル・ビヘイビアって呼んでるの
![公式投稿の引用カード。図中テキストは英語で『Novel behavior observed: solved environments never beaten before』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/079_official_post_quote.png)
- 🦜 きなこ：ARC Prizeは公式の投稿でも、これまで誰も突破できなかった環境を解く新しい動きが見られたって書いてるの
![ARC Prize 公式の評価コメント『demonstrating strong logical reasoning』を引用したカード](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/081_logical_reasoning_quote.png)
- 🦜 きなこ：強い論理的な推論を示した、っていう書き方なの。点が伸びたじゃなくて、解き方を褒めてるんだよ
- 🦜 きなこ：点数だけなら、数字が伸びたで済むもんね。行動について書き足したのが引っかかるところなの

## 同じ発表に混ざっていた「自社ベンチ」の数字

- 🦜 きなこ：そう思うよね。私も並んでたら同じ重さで読んじゃう
![『Frontier-Bench v0.1』の見出しテロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/094_frontier_bench_headline.png)
- 🦜 きなこ：でもね。もうひとつの数字は、フロンティア・ベンチ v0.1 っていうテストのものなの
![Frontier-Bench v0.1 の比較バー（Opus 5 43.3% / GPT-5.6 Sol 34.4% / Fable 5 33.7%）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/095_frontier_bench_bars.png)
- 🦜 きなこ：Opus 5が43.3%。GPT-5.6 Solが34.4%で、Fable 5が33.7%だよ
- 🦜 きなこ：じゃあ聞くね。このテスト、誰が作ったと思う？
![見出しテロップ。図中テキストは英語で『Frontier-Bench v0.1』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/099_frontier_bench_headline2.png)
- 🦜 きなこ：Anthropic自身なの。作ったのもAnthropic、測ったのもAnthropic
![測定フロー図。図中テキストは英語で『mini-SWE-agent harness』『mean reward over 5 trials』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/101_measurement_flow_terms.png)
- 🦜 きなこ：嘘ってわけじゃないの。中身も公開されてて、ミニSWEエージェントっていう仕組みで5回試した平均で出してる

## 値札が動かなかったという事件

- 🦜 きなこ：白状するとね、私が発表を見て最初に二度見したの、点数じゃなくて値札のほうだったの
![価格比較表。図中テキストは英語で『Opus 4.8 $5/$25』『Opus 5 $5/$25』『unchanged』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/114_price_table_unchanged.png)
- 🦜 きなこ：100万トークンあたり、入力5ドル・出力25ドル。これ、前のOpus 4.8とまったく同じ数字なの
- 🦜 きなこ：もっちー、商売の話になると急に鋭いよね
![Opus 5 $5/$25 と Fable 5 $10/$50 を並べ、半額であることを示す図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/118_price_half_diagram.png)
- 🦜 きなこ：Fable 5が入力10ドル・出力50ドル。つまりOpus 5は、ちょうどその半額なの
![引用符付きテロップ。図中テキストは英語で『Anthropic own wording』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/120_anthropic_wording_quote.png)
- 🦜 きなこ：そこ、ちょっと気をつけて。Fable 5の半分のコストでフロンティア知能って言ってるのは、Anthropic自身の言葉なの
![提供プラットフォーム一覧カード（Claude Max / Claude Pro / API / Amazon Bedrock / Google Cloud / Microsoft Foundry）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/122_platform_list_card.png)
- 🦜 きなこ：発表と同じ日に、全部のプラットフォームで使えるようになってるの

## 今日から使う手順 — モデルIDとバージョン

![ターミナル画面: Claude Code の起動直後の画面。モデル選択メニューが開いている状態](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/130_terminal_model_menu.png)
- 🦜 きなこ：じゃあ実際にやってみるね。飼い主のタブレット借りて、Claude Codeを開くよ
![バージョン要件テロップ。図中テキストは英語で『Claude Code v2.1.219 or later required』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/132_version_requirement_card.png)
- 🦜 きなこ：まずバージョンの確認から。Opus 5を使うには、Claude Codeがv2.1.219以降じゃないと駄目なの
![モデル一覧に Opus 5 が表示されない旧版画面と、表示される新版画面の対比](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/134_old_vs_new_model_list.png)
- 🦜 きなこ：そもそも一覧に出てこないの。だから古いままだと、指定してるつもりで別のモデルを使い続けちゃう
![ターミナル画面: `claude update` を実行し、バージョンが更新されるログ出力（更新後バージョンをハイライト）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/136_terminal_update_log.png)
- 🦜 きなこ：だから先に、クロード・アップデートって打っておくの。これで最新版になるよ
![ターミナル画面: `opus` エイリアス指定が Opus 5 に解決される様子の図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/138_terminal_alias_resolve.png)
- 🦜 きなこ：やり方はふたつあるの。ひとつはopusって短く指定する方法。これで自動的にOpus 5が選ばれるよ
![ターミナル画面: フル名 `claude-opus-5` を指定してピン留めする例](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/139_terminal_pin_full_name.png)
- 🦜 きなこ：もうひとつは、クロード・オーパス・ファイブってフル名で書く方法。こっちは指定したモデルに固定されるの

## まとめ

- 🐹 もっちー：まだ答えが出てない部分って、さっきの新規行動の中身のこと？
![未解決の問い2点のテロップ。図中テキストは英語で『1. What the novel behavior actually was』『2. Independent verification of the in-house benchmark』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/148_two_open_questions.png)
- 🦜 きなこ：それもある。もうひとつは、あの43.3%を誰か別の人が確かめたのかどうか
![2軸のまとめ表。図中テキストは英語で見出し『Who built it?』『Who measured it?』、行に『ARC-AGI-3』『Frontier-Bench』](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V270/150_two_axis_summary_table.png)
- 🦜 きなこ：今日の話、ひとことにするね。同じ発表の数字でも、誰が作って誰が測ったかで重さが変わるの
- 🦜 きなこ：30.2%はテストを作った側が測って公開した数字。43.3%は作ったのも測ったのもAnthropic

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*