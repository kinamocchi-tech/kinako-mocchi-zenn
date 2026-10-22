---
title: AIが書いたコードの45%は危ない？公式プラグインClaude Securityを実際に入れて試した【解説記事】
emoji: 🤖
type: tech
topics:
- ai
- llm
- tech
published: true
---

# AIが書いたコードの45%は危ない？公式プラグインClaude Securityを実際に入れて試した

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [AIが書いたコードの45%は危ない？公式プラグインClaude Securityを実際に入れて試した](https://www.youtube.com/watch?v=_KEVwIE2ktg)
:::
@[youtube](_KEVwIE2ktg)

## この記事で分かること

- 🐹 もっちー：きなこ、最近ぼく、コードのほとんどをAIに書いてもらってるんだけど、これって危なくないの？
- 🐹 もっちー：え、じゃあ残りの45%は危ないってこと？急に怖くなってきたんだけど
![Side-by-side comparison of the 45 percent and 12 percent figures](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/007_side_by_side_comparison_of_the_45_percen.png)
- 🐹 もっちー：45%と12%って、ぜんぜん違うよね。どっちが本当なの？
- 🦜 きなこ：そこが今日の入口なの。この2つの数字ね、測ってるものがそもそも違うんだよ

## 数字の正体 — 45%と12%はどう違うのか

![Comparison table of the two studies: denominator, target, source type](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/013_comparison_table_of_the_two_studies_deno.png)
- 🦜 きなこ：さっきの2つの数字ね、そもそも数えてる対象が違うの。まずVeracodeの45%から
![Branch diagram: safe option versus insecure option at the same decision point](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/014_branch_diagram_safe_option_versus_insecu.png)
- 🦜 きなこ：こっちは「安全な書き方が存在する場面で、モデルが危ないほうを選んだ割合」。つまり選択のミスを数えてるの
![Breakdown chart: 861 of 7,117 analyzable files flagged](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/016_breakdown_chart_861_of_7_117_analyzable_.png)
- 🦜 きなこ：こっちはファイル単位。解析できた7117ファイルのうち、861ファイルに脆弱性が見つかった。だから12%なの
- 🦜 きなこ：そう。だから45%と12%を並べて「どっちが正しい」って比べるのは、そもそも無理なの
![Comparison chart with icons separating vendor research from a preprint](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/019_comparison_chart_with_icons_separating_v.png)
- 🦜 きなこ：出どころも違うよ。Veracodeはセキュリティ企業の自社研究、arXivのほうは査読前の論文。どっちも「ゼロじゃない」とは言ってるけどね
- 🦜 きなこ：それがね、作った側のAnthropic自身が7月に出してるの。しかも外部サービスに送るんじゃなくて、いつも使ってるあの画面の中で完結する形で

## Claude Securityとは何者か — セッションの中で完結するスキャナ

![Plugin info card: claude-security v0.10.0, Anthropic Verified badge](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/023_plugin_info_card_claude_security_v0_10_0.png)
- 🦜 きなこ：名前はClaude Security。Anthropic公式のプラグインで、バージョンは0.10.0。2026年7月21日から22日ごろにベータ公開されたの
![Multi-agent flow diagram: map architecture, build threat model, hunt, independent review](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/025_multi_agent_flow_diagram_map_architectur.png)
- 🦜 きなこ：いいところに気づいたね。だからこのプラグイン、1体で見てないの。複数のエージェントが役割を分けて動くんだよ
![Step diagram highlighting the four stages one after another](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/026_step_diagram_highlighting_the_four_stage.png)
- 🦜 きなこ：まずコードベースの構造を把握して、次に脅威モデルを組み立てる。そのうえで脆弱性を探して、最後に見つけたものを別のエージェントが独立に検証するの
![Decision flow: a finding that can be refuted is labeled a false positive](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/028_decision_flow_a_finding_that_can_be_refu.png)
- 🦜 きなこ：そう、狙いはまさに誤検知を減らすこと。READMEでは、検証役は発見を反証しにいって、実際の攻撃経路を確認できなければ誤検知と呼ぶように指示されてるって書いてあるの
![Icon grid of the four focus categories: memory corruption, injection, auth bypass, complex logic bugs](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/030_icon_grid_of_the_four_focus_categories_m.png)
- 🦜 きなこ：重点は深刻度の高いところ。メモリ破損、インジェクション、認証バイパス、それから複雑なロジックのバグ、なの
![Quotation card labeled 'vendor claim'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/031_quotation_card_labeled_vendor_claim.png)
- 🦜 きなこ：ここ1つ注意ね。「パターンマッチ型のツールが見逃すものを見つける」っていうのは、Anthropic自身がそう説明してる、って言い方が正確なの

## 実際に使ってみる — インストールから3つの操作、そしてパッチ

![Terminal-style display of the install command](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/035_terminal_style_display_of_the_install_co.png)
- 🦜 きなこ：インストールはコマンド1本。スラッシュ plugin install claude-security アットマーク claude-plugins-official、だよ
![Checklist of the three prerequisites](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/036_checklist_of_the_three_prerequisites.png)
- 🦜 きなこ：前提は3つ。Claude Code本体と、Python 3.9以上、それからGitのチェックアウト。差分スキャンとパッチ提案にGitを使うからなの
![Menu diagram of the three operations: scan codebase, scan changes, suggest patches](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/038_menu_diagram_of_the_three_operations_sca.png)
- 🦜 きなこ：スラッシュ claude-security でメニューが開くの。できることは3つ。全体スキャン、変更スキャン、それからパッチ提案
![Workflow diagram: full scan first, diff scans afterwards](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/039_workflow_diagram_full_scan_first_diff_sc.png)
- 🦜 きなこ：使い分けはこう。最初の1回は全体スキャン。そのあとは、ブランチの差分やPRの差分だけを見る変更スキャンを回すの
![Mockup of a findings report screen](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/041_mockup_of_a_findings_report_screen.png)
- 🦜 きなこ：レポートが出るよ。そこから直したいものを選ぶと、パッチファイルを作ってくれるの
![Quotation card: 'Patches are never applied automatically'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/043_quotation_card_patches_are_never_applied.png)
- 🦜 きなこ：ううん、そこが違うの。パッチは自動では当たらない。ファイルとして出てくるだけなの

## 紛らわしい2つ — security-guidanceと、存在しない機能名

![Comparison table placing the two plugins side by side](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/052_comparison_table_placing_the_two_plugins.png)
- 🦜 きなこ：それ、別物なの。security-guidanceは、もっと軽いほうのプラグインだよ
![Flow diagram of a lightweight review that fixes issues before the pull request](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/053_flow_diagram_of_a_lightweight_review_tha.png)
- 🦜 きなこ：こっちはね、セッションの中でClaude自身が自分の変更をレビューして、PRに出す前にインジェクションや危ないDOM操作を直しちゃうタイプなの
![Requirement comparison table: CLI 2.1.144+ with Python 3.7+ versus Python 3.9+](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/054_requirement_comparison_table_cli_2_1_144.png)
- 🦜 きなこ：前提条件も違うの。security-guidanceはCLIが2.1.144以上でPythonは3.7以上。さっきのClaude SecurityはPython 3.9以上だったよね
![Diagram contrasting 'deep scanner' with 'lightweight in-line fixer'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/056_diagram_contrasting_deep_scanner_with_li.png)
- 🦜 きなこ：そう。深く探すスキャナがClaude Security、書いてる横で軽く直すのがsecurity-guidance。こう覚えておくといいよ
![Highlighted CHANGELOG line with the phrase 'safer auto mode' struck through](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/058_highlighted_changelog_line_with_the_phra.png)
- 🦜 きなこ：それはね、公式の機能名じゃないの。CHANGELOGを見ると、書いてあるのは「auto modeの改善」なんだよ
![Timeline marking July 20 and July 22](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/060_timeline_marking_july_20_and_july_22.png)
- 🦜 きなこ：セキュリティの話は名前の精度がそのまま設定の精度になるから、ここは丁寧にいこうね。……で、本体側もこの7月、静かに2つ動いてるの

## 本体側の守り — filesystem isolationとauto modeの改善

![Timeline of versions and dates: v2.1.216 on July 20, v2.1.218 on July 22](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/061_timeline_of_versions_and_dates_v2_1_216_.png)
- 🦜 きなこ：正直に言うとね、私も最初はプラグインの話だけだと思ってたの。でも本体のCHANGELOGを追いかけたら、同じ週に土台のほうも動いてたんだよ
![Code display of the setting key sandbox.filesystem.disabled](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/062_code_display_of_the_setting_key_sandbox_.png)
- 🦜 きなこ：1つめは7月20日のv2.1.216。sandbox.filesystem.disabledっていう設定が増えたの
![Boundary diagram separating the working directory from everything outside it](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/064_boundary_diagram_separating_the_working_.png)
- 🦜 きなこ：逆なの。切る設定がわざわざ用意されたってことは、ふだんは分離が効いてるってことだからね
![Diagram of the per-OS implementation: sandbox-exec and bubblewrap](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/065_diagram_of_the_per_os_implementation_san.png)
- 🦜 きなこ：中身はね、作業ディレクトリの中は読み書きOK、その外のファイルは触らせない、っていう仕組み。macOSならsandbox-exec、Linuxならbubblewrapで実現してるの
![Diagram of a prompt injection attempt stopped at the sandbox boundary](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/067_diagram_of_a_prompt_injection_attempt_st.png)
- 🦜 きなこ：そういうこと。変な指示を読まされたときでも、大事なファイルまで手が届かないようにする狙いなの
![Decision flow of auto mode with the classifier making the call](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/068_decision_flow_of_auto_mode_with_the_clas.png)
- 🦜 きなこ：2つめは7月22日のv2.1.218。危ないrmとか、バックグラウンド実行とか、あやしいWindowsパスの判定を、分類器が裁くようになったの

## まとめ

![Callback to the opening donut chart of 55 percent and 45 percent](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/071_callback_to_the_opening_donut_chart_of_5.png)
- 🦜 きなこ：最初の数字に戻るね。安全だったのは55%、危ない選択が45%。でもこれ、AIに書かせるのをやめる理由にはならないの
![Process diagram with a red cross on the step 'ship without any review'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/072_process_diagram_with_a_red_cross_on_the_.png)
- 🦜 きなこ：問題は書かせること自体じゃなくて、書かせた後を誰も見ないまま通しちゃうこと、なんだよ
- 🐹 もっちー：じゃあぼくは、明日から何をすればいいの
![Three-step summary: install, scan the diff, review the patch yourself](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V266/074_three_step_summary_install_scan_the_diff.png)
- 🦜 きなこ：最小の一歩は3つだけ。プラグインを入れて、PRを出す前に変更スキャンをかけて、出てきたパッチは自分で読んでから当てる。これだけなの

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*