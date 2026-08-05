---
title: 119Bなのに実質6.5B！Mistral Small 4が示すOSS LLM新基準【解説記事】
emoji: 🤖
type: tech
topics:
- moe
- ai
- llm
- tech
published: true
---

# 119Bなのに実質6.5B！Mistral Small 4が示すOSS LLM新基準

> 🐹🦜 **この記事に登場する2匹**
>
> - 🐹 **もっちー** （ハムスター）… AI はまだ勉強中。「それどういうこと？」と素朴に質問する生徒役
> - 🦜 **きなこ** （セキセイインコ）… AI で調べものをこなす解説役。やさしく深掘りして教える先生役
>
> この記事は2匹の掛け合いを書き起こした形式です。発言の先頭にいる絵文字＋名前が話者です。

:::message
📺 この記事は YouTube「きなこもっちーのテック深掘り」の動画解説記事です。
動画はこちら: [119Bなのに実質6.5B！Mistral Small 4が示すOSS LLM新基準](https://www.youtube.com/watch?v=sOkJh6rcl-c)
:::

## この記事で分かること

- 🐹 もっちー：AIって、推論用・画像認識用・コーディング用でモデルを使い分けるのが普通でしょ？
- 🐹 もっちー：1つに統合！？そんなことできるの！？
- 🐹 もっちー：119Bあるのに6.5B？意味わからんのやけど！
- 🦜 きなこ：今日はその仕組みと、ヨーロッパの重工業がこぞって採用した理由まで、全部深掘りしていくね

## ユニファイド・アーキテクチャの正体

![Magistral（推論）・Pixtral（画像）・Devstral（コーディング）の3モデルが1つに統合される図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/015_moe_unify.png)
- 🦜 きなこ：Small 4はね、推論が得意なMagistral、画像を見るPixtral、コーディング担当のDevstral、この3つの力を1個にまとめちゃったの
- 🦜 きなこ：そう、それがユニファイド・モデルって呼ばれてるの。もう用途ごとにいちいちモデルを選んで切り替える手間が、まるっと消えたんだよ
![総パラメータ119B・アクティブ6.5Bを対比した図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/019_param_compare.png)
- 🦜 きなこ：普通はそう思っちゃうよね。でもね、モデル全体の容量は119Bって巨大なのに、実際に一度に動くのはそのうちのほんの一部だけなの
![128の専門家パーツのうち4つだけが点灯するMoEルーティング図](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/020_moe_routing.png)
- 🦜 きなこ：モデルの中には128個の専門パーツが並んでいて、質問が来るたびに、その中のたった4個だけが起動する仕組みなんだよ
![総合病院で症状に応じた専門医だけが診察に出るイラスト](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/022_hospital_metaphor.png)
- 🦜 きなこ：その違和感、すごく大事なポイントだよ。これはMoEっていう仕組みでね、総合病院をイメージすると一気に腑に落ちるの
- 🦜 きなこ：病院に患者さんが来ても、全部の科の先生が集まって診るわけじゃないでしょ。症状に合った専門医だけが呼ばれて診察するの

## ベンチマークと価格破壊の現実

- 🦜 きなこ：それがね、正直に言うとSmall 4は最高スコアじゃないんだよ。むしろ勝ってないのに世界中から注目されてる、そこがこのモデルのすごく面白いところなの
![スコアバー図: MMLU-Pro 78.0% / GPQA Diamond 71.2%（Mistral Small 4）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/031_score_bar_mistral.png)
- 🦜 きなこ：まず点数を見るとね、難しいMMLU-Proで78.0%、大学院レベルの科学を問うGPQA Diamondで71.2%を記録してるの。数字だけ見ればかなり優秀なんだよ
![比較図: Gemma 4 12B 78.8% > Small 4 71.2%（小さいモデルが上回る）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/033_gemma_vs_small.png)
- 🦜 きなこ：ところがね、ライバルのGemma 4 12BはGPQA Diamondで78.8%。ずっと小さいモデルなのに、Small 4より上に来てる場面もあるの
- 🦜 きなこ：ううん、そこが誤解されがちなところなの。Small 4の本当のすごさは「点数の高さ」じゃなくて、「同じ答えをどれだけ短く出せるか」にあるんだよ
![出力文字数比較: 同じAA LCR 0.72 を Qwen 約6000字 / Small 4 約1600字で達成](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/036_output_length_compare.png)
- 🦜 きなこ：長い文章を読ませるテストで0.72点なんだけど、ライバルのQwenが6千文字も書くところを、Small 4はたった1600文字で同じ点を出しちゃうの
![DeepSeek V4-Pro API価格75%カット / 100万トークン 入力$0.435・出力$0.87](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/038_deepseek_price.png)
- 🦜 きなこ：そういうこと。しかも今のOSSの世界は点数より「価格」の勝負に移ってて。DeepSeekは100万トークンで入力0.435ドルまで、料金を75%も下げたの

## Voxtral TTSが変えるゼロショット音声クローン

- 🦜 きなこ：さて次はガラッと話題を変えて、Mistralが音声の世界にも打ち込んだ一手、Voxtral TTSっていう音声合成の新技術を、じっくり深掘りしていくね
![Voxtral TTS｜4Bパラメータ・3秒の参照音声でゼロショット音声クローン](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/044_voxtral_intro.png)
- 🦜 きなこ：そうそう、その進化版なの。Voxtralのすごいところは、たった3秒のお手本の声を聞かせるだけで、その人の声質をそっくり再現できちゃう、まさにゼロショットの技術なんだよ
![比較｜VOICEVOX＝手動チューニング前提 / Voxtral＝お手本3秒でゼロショット](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/046_voxtral_vs_voicevox.png)
- 🦜 きなこ：そこが決定的な違いなの。従来の音声合成ソフトは手動チューニングが前提だけど、Voxtralはお手本を渡すだけで、声質も感情もアクセントもAIが自動でマネしてくれるの
![ElevenLabs｜声のクローンに参照音声30秒が必要](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/048_elevenlabs_compare.png)
- 🦜 きなこ：気持ちは分かる。でね、ライバルの音声AI大手ElevenLabsは、声のクローンを作るのに、なんと30秒ぶんのお手本を必要とするんだよ
![多言語ブラインドテスト｜Voxtral勝率68.4%（スペイン語87.8%）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/050_voxtral_winrate.png)
- 🦜 きなこ：そういうこと。しかも9言語での多言語ブラインドテストで、ElevenLabs相手に68.4%の勝率を出して、特にスペイン語では87.8%も勝ったんだよ
![ライセンス｜オープンウェイト版はCC BY-NC 4.0（非商用）](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/052_voxtral_license.png)
- 🦜 きなこ：ただこのVoxtral、オープンウェイト版は商用利用がちょっとややこしいライセンスになってるんだよね。仕事でうっかり勝手に組み込むと、あとで引っかかることがあるの

## Search ToolkitとOCR 4が終わらせる『配管工事』

![AIと社内データをつなぐRAGのイメージ図。パイプ（配管）で結ばれる様子](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/055_rag_pipe_diagram.png)
- 🦜 きなこ：いいところに引っかかったね。企業が自分の会社のデータをAIに検索させる仕組みをRAGって言うんだけど、それを一から作る作業が、まさに配管工事そっくりで大変なの
![取り込み・検索・評価の3本のパイプが並ぶ図解](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/057_three_pipes.png)
- 🦜 きなこ：まだ大丈夫、簡単に言うね。AIに社内の書類とかを読ませて、質問に答えさせる技術のこと。そのために、取り込み・検索・評価っていう3つの処理を、順番に繋いでいく必要があるんだよ
![Diagram contrasting manual pipe-connecting (old way) vs Search Toolkit's unified system, with 'Released May 28, 2026' badge in English](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/059_manual_vs_toolkit.png)
- 🦜 きなこ：今まではLangChainなんかで、開発者が3本の管を手作業で繋いでたの。数週間かかることもあってね。それを標準化したのが、5月公開のSearch Toolkitなんだよ
![Diagram of OCR 4 extracting tables, formulas, and position data from documents, with English badge '170 languages / $4 per 1000 pages'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/061_ocr_extraction.png)
- 🦜 きなこ：そうなの。その配管の入り口を担うのがOCR 4。書類を撮るだけで、表や数式の位置まで正確に見分けて、なんと170言語に対応。しかも千ページ4ドルっていう安さなんだよ
![Teaser transition to next theme: 'AI Company Acquires Unrelated Industry!?' banner in English](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/063_acquisition_teaser.png)
- 🦜 きなこ：でしょ？でも実はね、この後の話が一番びっくりするところなの——MistralはAIの会社なのに、全然違う業界の会社を、まるごと買収しちゃったんだよ
![Title card reading 'Search Toolkit: Ending the RAG Plumbing Work' displayed in English](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/054_search_toolkit_title.png)
- 🐹 もっちー：ちょっと待って、きなこ。さっき配管工事を終わらせるって言ってたよね？これAIの話だよね？なんで急に、水道屋さんみたいな工事の話が出てくるの？意味わからないんだけど

## Emmi買収とPhysics AIの衝撃

![画面切替：Mistralのロゴと「2026年5月 衝撃の発表」テロップ](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/064_mistral_announcement.png)
- 🦜 きなこ：さっきのデータ検索を楽にするツールも十分驚きだったけど、2026年5月にMistralが出した発表は、それをはるかに超えて業界を騒がせる衝撃的なものだったの
![Headline banner 'Mistral x Emmi AI Acquisition' with 'Physics AI' keyword, in English](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/066_emmi_acquisition.png)
- 🦜 きなこ：なんとね、オーストリアのEmmi AIっていう「物理AI」を専門にする研究者集団を、まるごと買収したの。この発表には私も最初はさすがに自分の目を疑ったよ
![Large banner showing acquisition price 'approx. ¥54B JPY (EUR 330M)' in English](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/068_acquisition_price.png)
- 🦜 きなこ：それがまさにその通りなの。買収額はなんと3億3,000万ユーロ、日本円にしておよそ540億円。飛行機や車を設計するための、ゴリゴリの重工業の技術なんだよ
![Map pin on Linz, Austria with English caption '35+ researchers joined'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/070_linz_map.png)
- 🦜 きなこ：新しい研究拠点はオーストリアのリンツで、35人以上の研究者がチームごとまるごと合流したの。実はこの買収の背景には、ヨーロッパならではの深い事情もあってね
![図解：物理ソルバーの出力→学習→形状から挙動を予測](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/072_physics_solver_diagram.png)
- 🦜 きなこ：LLMが大量の文章を読んで言葉を学ぶのと同じで、物理AIは物理計算の結果をたくさん学んで、形と条件を入れるだけで、その挙動そのものを一気に直接予測できるの
![Before/after diagram of Airbus wing CFD analysis showing 'Hours to Seconds' in English](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/074_airbus_cfd.png)
- 🦜 きなこ：そう近いね。エアバスの翼まわりの気流計算は、昔はスパコンを使っても数時間から数日かかってたのが、この物理AIでたった数秒で終わるようになったの

## OSS三強比較と主権AI戦略

![OSS LLM三強マップ：Meta・Google・Mistralの3ロゴを三つ巴で配置](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/077_oss_llm_triangle.png)
- 🦜 きなこ：ここまでMistralを見てきたけど、実は今のオープンソースのAIって、大きく三つの勢力に分かれてて、それぞれ全然違う方向で自分の強みを磨いて競い合ってるんだよ
![Meta Llama 4 Scout：MoE・109B総/17Bアクティブ・規模主導](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/079_llama4_scout.png)
- 🦜 きなこ：一つ目はMeta。Llama 4のScoutっていうモデルで、必要な専門家だけを動かすMoE方式を使って、とにかく力技の圧倒的な規模で勝負を仕掛ける戦略なの
![10,000,000トークンの長大コンテキストを強調表示](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/080_long_context.png)
- 🦜 きなこ：なんと一度に読める文章量が最大1000万トークン。分厚い本を何十冊も丸ごと渡せるレベルで、長い文章の理解でクローズドなAIに真っ向勝負を挑んでるんだよ
![Llama Community License：7億MAU超で商用制限](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/082_llama_license.png)
- 🦜 きなこ：ただしLlamaには意外と大きな落とし穴があってね。月間7億人ものユーザーを超える巨大企業は、商用で使うときにライセンスの特別な制限がかかっちゃう決まりなの
![Google Gemma 4 12B：エンコーダレス・16GB VRAMでローカル実行](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/084_gemma4_card.png)
- 🦜 きなこ：二つ目はGoogleのGemma 4。重い変換装置を挟まず画像や音声を直接読み込む仕組みだから遅れが少なく、16GBのノートPC一台でもローカルで動かせるのが強みなの
![Mistral Small 4：Apache 2.0・119B総/6.5Bアクティブ・自己ホスト効率](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/086_mistral_small4_card.png)
- 🦜 きなこ：そこが一番の核心なの。MistralのSmall 4はApache 2.0で商用も完全に無制限。しかも119Bあるのに実際に動くのは6.5Bだけで、とても軽く動くの

## まとめ

![Diagram connecting Small 4, Voxtral, Search Toolkit, and Emmi with English label 'Mistral Ecosystem'](https://pub-2687e67855c941a0a1a9e1ad51ffc967.r2.dev/images/V190/090_ecosystem_diagram.png)
- 🐹 もっちー：バラバラに見えてた発表が、実は全部繋がってたんだね
- 🦜 きなこ：そう。Small 4・Voxtral・Search Toolkit・Emmi、どれも単発の製品じゃなくて、Apache 2.0を軸にした一つの経済圏を作る戦略なんだよね
- 🐹 もっちー：へー、そう考えると見え方変わるな
- 🦜 きなこ：しかもApache 2.0だから商用利用のハードルが低くて、事業として使い倒せる自由度も大きいポイントなの

---

*ハムスターのもっちーとセキセイインコのきなこの掛け合い形式でテックを深掘りする YouTube チャンネル。*
*チャンネル登録はこちら: https://www.youtube.com/@kinamocchi_tech*