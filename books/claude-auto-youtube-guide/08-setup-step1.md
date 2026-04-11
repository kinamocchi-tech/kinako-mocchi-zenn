---
title: "セットアップ Step 1 ── GitHubとClaude Codeの準備"
---

# セットアップ Step 1 ── GitHubとClaude Codeの準備

この章から、実際のセットアップ作業を始めます。
Step 1ではGitHubアカウントとClaude Codeの準備を行います。

## 所要時間の目安

- GitHubアカウント作成: 約10分
- リポジトリのセットアップ: 約20分
- Claude Codeの初期設定: 約15分

合計: 約45分

## 1-1. GitHubアカウントの作成

:::message
すでにGitHubアカウントをお持ちの場合は「1-2」にお進みください。
:::

1. [github.com](https://github.com) にアクセス
2. 右上の **[Sign up]** をクリック
3. メールアドレス・ユーザー名・パスワードを設定
4. メール認証を完了

**ユーザー名のアドバイス**: 後から変更できますが、
GitHubのURLに含まれるため、シンプルで覚えやすいものを選びましょう。

## 1-2. リポジトリの作成

本書のテンプレートリポジトリをコピーして使います。

:::message
テンプレートリポジトリは現在準備中です。
公開後は本書のサポートページでURLをお知らせします。
それまでは下記「手動でリポジトリを作成する場合」の手順をお使いください。
:::

### 手動でリポジトリを作成する場合

1. GitHubにログインした状態で、右上の **[+]** → **[New repository]** をクリック
2. リポジトリ名を入力（例: `my-youtube-channel`）
3. **Private**（非公開）を選択（APIキーが関係するため公開設定は非推奨）
4. **[Create repository]** をクリック

## 1-3. Claude Codeにアクセスする

1. [claude.ai/code](https://claude.ai/code) にアクセス
2. Claudeアカウントでログイン（Pro/Max プランが必要）
3. **[New project]** をクリック
4. 作成したGitHubリポジトリと連携する

## 1-4. CLAUDE.mdの初期設定

リポジトリのルートに `CLAUDE.md` ファイルを作成します。

本書の場合、CLAUDE.mdは非常に詳細なファイルですが、
最初は以下の最小構成から始めましょう。

```markdown
# CLAUDE.md

## プロジェクト概要
YouTubeチャンネルの自動制作パイプライン。

## 応答スタイル
- 日本語で応答する
- 本題から入る（前置きを省略）

## やってはいけないこと
- mainブランチに直接pushしない
- ユーザーの承認なしに動画を公開しない
```

成長とともに、CLAUDE.mdにルールを追加していきます。

## 1-5. Scheduled Tasksの初期設定

1. Claude Codeの画面左サイドバーから **[Scheduled Tasks]** を開く
2. **[Add scheduled task]** をクリック
3. 以下を設定する:

| 項目 | 設定値 |
|------|--------|
| 実行間隔 | 1 hour（毎時間） |
| プロンプト | （第4章の時刻ルーティング表に従う指示文） |

:::message
Scheduled Tasksのプロンプトには `docs/rules/hourly-routing.md` の指示に従って動作するよう記述します。詳細は第18章（スケジュール設計）で説明します。
:::

## セットアップ Step 1 チェックリスト

- [ ] GitHubアカウントを作成した
- [ ] リポジトリを作成した（private設定）
- [ ] Claude Codeにログインした
- [ ] GitHubリポジトリとClaude Codeを連携した
- [ ] CLAUDE.mdの最小構成を作成した
- [ ] Scheduled Tasksを1時間ごとに設定した

次のStep 2では、YouTube・Gemini・VOICEVOXのAPIキーを取得・設定します。
