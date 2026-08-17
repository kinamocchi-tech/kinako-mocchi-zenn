---
title: AIが壊したファイルを戻す方法｜Claude Code /rewindの落とし穴【解説記事】
emoji: 🤖
type: tech
topics:
- rewind
- claude
- git
- ai
- llm
published: true
---

# AIが壊したファイルを戻す方法｜Claude Code /rewindの落とし穴

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [AIが壊したファイルを戻す方法｜Claude Code /rewindの落とし穴](https://www.youtube.com/watch?v=W5D1_RH43JI)
:::

## この記事で分かること

- 🐹 もっちー：ねえきなこ、AIに任せた作業のやり直しって、チャットを巻き戻すだけでしょ？
- 🐹 もっちー：えっ、ファイルが戻る？ さっき書いたやつが消えるってこと？
![Roadmap telop with five numbered items in English: '1. When checkpoints are created', '2. What never comes back', '3. Rewind vs Fork', '4. Checkpoints vs Git', '5. After you close the session'.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/006_roadmap_telop_with_five.png)
- 🦜 きなこ：今日はね、この巻き戻しがどこまで届くのか、逆に何は絶対に戻らないのかを、最後まで見ていくよ
- 🐹 もっちー：はっ？ 同じフォルダの中で半分だけ戻るってこと？ それ怖くない？

## チェックポイントは「毎回」できている

![Horizontal timeline where each user prompt stacks a new save point marker, labeled in English: 'Prompt 1 -> checkpoint', 'Prompt 2 -> checkpoint', 'Prompt 3 -> checkpoint'.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/021_horizontal_timeline_where_each.png)
- 🦜 きなこ：そこはね、公式ドキュメントがはっきり書いてるの。プロンプトを送るたびに、保存点がひとつ作られるって
![Two-step diagram: a file icon is copied into a snapshot box first, then the original is edited. English labels 'snapshot before change' and 'then edit'.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/023_two_step_diagram_a.png)
- 🦜 きなこ：しかもね、Claudeはファイルを書き換える前に、毎回そのファイルの写しを取っておくの
- 🦜 きなこ：そういうこと。だから保存し忘れは、そもそも起きないようになってるの
![Terminal-style card showing two entry points side by side in English: 'Type /rewind' and 'Press Esc twice (empty input)'.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/029_terminal_style_card_showing.png)
- 🦜 きなこ：呼び出し方は二つあってね、スラッシュrewindと打つか、入力欄が空のときにEscを二回押すの
- 🦜 きなこ：入力欄が空のときだけね。文字が残ってると、そっちの取り消しになるよ
![Menu card listing four options in English: 'Restore code and conversation', 'Restore conversation only', 'Restore code only', 'Summarize from selected message'.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/032_menu_card_listing_four.png)
- 🦜 きなこ：そこでメニューが開くとね、選べる項目が四つ並んでるの

## 戻らないもの — Bash で作った変更

- 🦜 きなこ：そう思うよね。私も最初は、それで十分だと思ってたの
- 🦜 きなこ：でもね、戻せるのは Claude が自分の編集ツールで書いたときだけなの
![Two-column comparison card. Left column header 'Tracked' listing 'Write', 'Edit', 'NotebookEdit'. Right column header 'Not tracked' listing 'Bash commands', 'External processes', 'Manual edits'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/051_two_column_comparison_card.png)
- 🦜 きなこ：公式ドキュメントにも、追跡されるのは Write と Edit と NotebookEdit の3つだけって書いてあるの
- 🦜 きなこ：Claude がその道具を使う直前に、ファイルの中身が丸ごと控えられるんだよ
![Three tool chips grouped inside one box labeled 'Claude's own writing tools', each chip reading 'Write', 'Edit', 'NotebookEdit'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/054_three_tool_chips_grouped.png)
- 🦜 きなこ：名前は覚えなくていいよ。全部、Claude が自分の手で書き込むための道具なの
![Simple illustration: a hamster cage rearranged by its own occupant, with a small dotted 'memo' note beside it showing the moved items. No characters drawn](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/055_simple_diagram_a_small.png)
- 🦜 きなこ：もっちーが自分でケージの中を模様替えするのと同じ。どこを動かしたか、自分で覚えてるでしょ

## /fork は巻き戻さない — 増やすコマンド

- 🦜 きなこ：失敗したところまで戻したくて、それを打ったところを想像してみて
![Timeline with the playhead staying exactly where it was, English caption 'nothing moved backwards'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/083_timeline_with_the_playhead.png)
- 🦜 きなこ：元のセッションは、そのまま残ってるの。何も戻ってないんだよ
![Two arrows side by side. Left arrow points backward on a timeline, labeled 'rewind'. Right arrow branches upward from the present point into a second parallel line, labeled 'fork'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/085_two_arrows_side_by.png)
- 🦜 きなこ：今の会話がまるごとコピーされて、もう一つ増えたの
![Two word cards facing each other. Left card reads 'rewind = go back'. Right card reads 'fork = add a branch'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/087_two_word_cards_facing.png)
- 🦜 きなこ：そう。リワインドは戻す、フォークは増やす。この一語の違いだけ覚えればいいの
![Agent list UI mockup. An existing row stays highlighted as 'original session' and a new row appears below it labeled 'forked background session'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/088_agent_list_ui_mockup.png)
- 🦜 きなこ：コピーは裏側で動く別のセッションになって、エージェントの一覧に自分の行を持つの
- 🦜 きなこ：元の方は何も変わらないまま、そこから先は二つが別々に進んでいくんだよ

## local undo と permanent history

![Two-column comparison table. Left column header 'local undo': rows 'inside one session', 'automatic', 'Bash changes not tracked'. Right column header 'permanent history': rows 'outlives the session', 'explicit', 'everything kept'.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/114_two_column_comparison_table.png)
- 🦜 きなこ：その気持ちは分かるよ。でも公式は、その二つをはっきり別物として書いてるの
![Quote card rendering the official sentence verbatim: 'Think of checkpoints as local undo and Git as permanent history'.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/115_quote_card_rendering_the.png)
- 🦜 きなこ：チェックポイントは local undo、Git は permanent history。そう位置づけてるんだよ
- 🦜 きなこ：そう。だから使い分けの決め手も、たった一つだけなの
![Two horizontal timelines meeting a vertical dashed line labeled 'session closed'. The upper timeline (checkpoints) stops at the line; the lower timeline (Git) continues past it.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/120_two_horizontal_timelines_meeting.png)
- 🦜 きなこ：セッションを閉じたあとに残るのはどっちか。それだけで決まるよ
- 🦜 きなこ：セッションの中の仕組みだからね。あとから見返す記録としては当てにできないの
![Illustration of a safety net stretched under a workbench, fading out at the right edge where a 'session end' marker stands.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/123_illustration_of_a_safety.png)
- 🦜 きなこ：作業してる間だけ張ってある安全網。そう思っておくとちょうどいいよ

## /clear のあとと、SDK 側の非対称

![Version card in English: 'v2.1.191 (2026-06-24) — /rewind can resume a conversation from before /clear was run'.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/141_version_card_in_english.png)
- 🦜 きなこ：そこも変わったの。6月24日の 2.1.191 から、消す前の会話を再開できるようになったんだよ
![Menu mockup where an entry above the '/clear' divider is still selectable, English caption 'the pre-clear session is still on the list'.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/143_menu_mockup_where_an.png)
- 🦜 きなこ：そう。消したあとでも、rewind のメニューから前の状態を選べるようになったの
![Two independent switches side by side, labeled 'conversation' and 'files', with only the conversation switch flipped.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/145_two_independent_switches_side.png)
- 🦜 きなこ：ただしそれは会話の話。ファイル側の線引きは、さっきのままなの
- 🦜 きなこ：そこは変わってないの。会話が戻せることと、ファイルが戻ることは別々に考えて
![Two-floor stack diagram. Upper floor labeled 'CLI you type into', lower floor labeled 'Agent SDK your program calls'.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/149_two_floor_stack_diagram.png)
- 🦜 きなこ：よく分かったね。実はもう一段、下の階の話があるの
- 🦜 きなこ：大丈夫、一言でいくね。Claude を自分のプログラムから動かすための道具があるの

## まとめ

- 🐹 もっちー：今日の話、ぼくの言葉でまとめてみていい？
- 🦜 きなこ：どうぞ。自分の言葉になってたら、それが一番あとまで残るよ
![Three-item takeaway card. Line 1: '/rewind = local undo for Write / Edit / NotebookEdit changes'. Line 2: '/fork = branch out, original session kept'. Line 3: 'Git = the only record that outlives the session'.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/170_three_item_takeaway_card.png)
- 🐹 もっちー：まず /rewind は、その場のやり直し。ファイルまで戻してくれるやつ
- 🐹 もっちー：/fork は戻さない。元を残したまま、枝を増やすほう
![Two-step loop diagram: box 'Try it under a checkpoint' arrow box 'If it holds, commit'. Caption below reads 'the default working rhythm'.](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V235/175_two_step_loop_diagram.png)
- 🦜 きなこ：持ち帰りの一番手はこれ。チェックポイントで試して、通ったらコミットする

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*