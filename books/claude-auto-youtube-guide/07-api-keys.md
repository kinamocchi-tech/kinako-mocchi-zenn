---
title: "APIキーと環境変数 ── 安全な設定方法（非エンジニア向け）"
---

# APIキーと環境変数 ── 安全な設定方法（非エンジニア向け）

## APIキーとは

**APIキー** とは、外部サービスを使うための **「合言葉（パスワード）」** です。

例えば、YouTube APIを使って自動アップロードするには、
「このリクエストはあなたのYouTubeアカウントから送られたものです」と証明する必要があります。
その証明に使うのがAPIキーです。

:::message alert
APIキーは **絶対に他人に見せてはいけません**。
クレジットカード番号と同じくらい大切なものです。
本書では、APIキーをGitHubの「Repository Secrets（リポジトリシークレット）」に安全に保存する方法を採用しています。
:::

## 本書で使うAPIキー一覧

| サービス | 用途 | 料金 | 必須/任意 |
|---------|------|------|--------|
| **GitHub Personal Access Token** | GitHubへのアクセス | 無料 | **必須** |
| **YouTube Data API v3（OAuth）** | 動画アップロード・スケジュール管理 | 無料（1日10,000ユニット） | **必須** |
| **Gemini API** | 画像生成（Gemini Flash） | 無料枠あり（1日1,500リクエスト） | **必須** |
| **VOICEVOX** | 音声合成 | **完全無料**（APIキー不要） | **必須** |
| **Slack Bot Token** | 進捗通知・レポート | 無料プランで可 | 任意（推奨） |

:::message
Slack通知は任意ですが、**週次レポートをSlackで受け取ることで「Human-on-the-loop」が実現** します。
Slackを使わない場合は、GitHubのIssueを週１回手動で確認する運用になります。
:::

## 環境変数とは

**環境変数** とは、プログラムが参照できる「システム全体の設定値」です。

APIキーをコードの中に直接書くと、GitHubに公開したときに漏洩するリスクがあります。
代わりに「環境変数」として安全な場所に保存し、コードからはその変数名で参照します。

```
悪い例（コードに直接書く）:
  youtube_api_key = "AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXX"  ← 漏洩リスク

良い例（環境変数で参照）:
  youtube_api_key = os.environ["YOUTUBE_API_KEY"]  ← 変数名だけ書く
```

## GitHub Repository Secretsへの保存方法

本書では、APIキーを **GitHub Repository Secrets** に安全に保存します。

1. GitHubのリポジトリページを開く
2. **[Settings]（設定）** → **[Secrets and variables]** → **[Actions]** をクリック
3. **[Secrets]** タブを選択
4. **[New repository secret]** をクリック
5. 変数名（例: `YOUTUBE_REFRESH_TOKEN`）と値（APIキー）を入力して保存

:::message
「SecretsとVariablesの違いは？」
- **Secrets**: 一度保存すると値を再確認できない。APIキーなど機密情報の保存に適している
- **Variables**: 値を後から確認できる。公開しても問題ない設定値向き
APIキーのような機密情報は必ず **Secrets** で管理してください。
:::

## YouTube APIキーの取得手順

詳細は第9章（セットアップ Step 2）で説明しますが、手順の概要は以下のとおりです。

1. **Google Cloud Console** にアクセス
2. 新しいプロジェクトを作成
3. **YouTube Data API v3** を有効化
4. **OAuth 2.0 クライアントID** を作成（デスクトップアプリ）
5. **OAuth 2.0 Playground** で認証フローを実行して **Refresh Token** を取得

:::details OAuth認証とは
「OAuth（オーオース）」は安全な認証の仕組みです。
YouTubeにログインして「このアプリがあなたの代わりに動画をアップロードしてよいですか？」と許可を求めるプロセスです。
一度許可すると、**Refresh Token** という長期有効なトークンが発行されます。このトークンを環境変数に保存することで、以後は自動でYouTube操作が可能になります。

**OAuth 2.0 Playgroundでの手順**:
1. [OAuth 2.0 Playground](https://developers.google.com/oauthplayground/) にアクセス
2. 右上の歯車アイコン → 「Use your own OAuth credentials」をチェック
3. クライアントIDとクライアントシークレットを入力
4. スコープ選択で `https://www.googleapis.com/auth/youtube` を入力・選択
5. `Authorize APIs` → Googleアカウントでログイン → `Exchange authorization code for tokens`
6. 表示された **Refresh token** をコピーして `YOUTUBE_REFRESH_TOKEN` として保存
:::

## Gemini APIキーの取得手順（概要）

1. **Google AI Studio** にアクセス
2. 「Get API key」をクリック
3. 新しいAPIキーを作成
4. 取得したキーをGitHub Repository Variablesに `GEMINI_API_KEY` として保存

## セキュリティのまとめ

- APIキーはGitHub Repository Secretsに保存する（コードに書かない）
- APIキーを他人に見せない・チャットに貼り付けない
- 不審な使用量が発生したらすぐにAPIキーを再発行する
- 使わなくなったAPIキーは削除する

次の章から、いよいよ実際のセットアップ作業に入ります。
