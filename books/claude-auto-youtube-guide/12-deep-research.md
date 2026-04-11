---
title: "Phase 2 ディープリサーチ ── あなたが唯一やること"
---

# Phase 2 ディープリサーチ ── あなたが唯一やること

## このフェーズだけはあなたが実施します

本書のシステムで **唯一あなたが手動で行う作業** が、Phase 2のディープリサーチです。

:::message
**なぜここだけ手動なのか？**

Claude の「Research（リサーチ）機能」は非常に高品質なウェブ検索をしてくれますが、
**Claudeのチャット画面でのみ利用できる機能** です。
APIやScheduled Tasksからは呼び出せないため、人間が実行する必要があります。
:::

## Claudeのリサーチ機能とは

**Claudeのリサーチ機能（Research）** は、Claudeがウェブを検索・横断して
詳細な調査を行う機能です。

通常のウェブ検索と異なり、Claudeが複数のサイトを横断して情報を統合し、
信頼性の評価や矛盾の検出まで行ってくれます。

### リサーチ機能の使い方

1. [claude.ai](https://claude.ai) をブラウザで開く（Pro/Max プランにログイン）
2. 新しい会話を開始する
3. テキスト入力欄の左側にある **「リサーチ」ボタン（または "Research" アイコン）** をクリック
4. リサーチしたいテーマについてプロンプトを入力して送信

:::message alert
**重要な注意事項**

Claudeのリサーチ機能は、**ウェブチャット・Claude Desktop・Claude Mobileからのみ利用可能** です。

- APIからは利用できません
- Scheduled Tasksからは自動実行できません
- ブラウザの自動操作（RPA等）で動かすことはAnthropicの利用規約で禁止されています

出典: [Anthropicサポート公式ドキュメント](https://support.claude.com/en/articles/11088861-using-research-on-claude)

> "The feature is accessible through the web chat interface, Claude Desktop, and Claude Mobile applications only. It is not available via API."
:::

## リサーチプロンプトの書き方

GitHub IssueのPhase 2には **ディープリサーチ用のプロンプト** が自動生成されています。

```markdown
## Deep Research プロンプト

以下のプロンプトをClaudeのリサーチ機能に貼り付けてください:

---
「Claude Sonnet 4.6の新機能『Adaptive Thinking』について詳しく調査してください。
以下の観点で情報を収集・整理してください:

1. 機能の詳細（何ができるようになったか）
2. 従来版との違い（比較）
3. 実際の使用例・ユースケース
4. 開発者コミュニティの反応
5. 利用上の注意点・制限事項
6. 公式発表日・バージョン番号・価格変更の有無

信頼できる一次ソース（公式ブログ・論文・公式ドキュメント）を優先してください。
推測で情報を補完せず、不明な点は『要確認』と明記してください。」
---
```

このプロンプトをそのままコピーしてClaudeに貼り付けるだけでOKです。

## リサーチ結果の保存方法

リサーチ完了後、Claudeの回答をコピーして
GitHubのリポジトリに保存します。

保存先: `content/research/V{動画ID}_research.md`

Claude Codeのチャットで以下を実行することもできます:

```
「このリサーチ結果を content/research/V005_research.md として保存してください」
```

Claude Codeが自動でファイルを作成・保存します。

## 所要時間の目安

| 作業 | 時間 |
|------|------|
| リサーチプロンプトを確認・コピー | 2分 |
| Claudeのリサーチ機能で実行 | 5〜15分（Claudeが自動実行） |
| 結果をリポジトリに保存 | 3分 |

**合計: 約10〜20分/本**

これがあなたの唯一の定期作業です。

## リサーチ機能が利用できるプラン

| プラン | Researchリサーチ機能 |
|--------|-------------------|
| Free | 限定的（回数制限あり） |
| Pro | 利用可（回数制限あり） |
| Max | 利用可（余裕あり） |
| Team/Enterprise | 利用可 |

:::message
Researchリサーチ機能はPro以上のプランで利用できます。本書のシステム全体を動かすにはMax プランを推奨しているため、リサーチ機能も十分に使えます。
:::

次の章では、リサーチ結果をもとに **台本が自動生成される仕組み（Phase 3）** を解説します。
