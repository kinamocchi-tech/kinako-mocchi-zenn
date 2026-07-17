---
title: "セットアップ Step 2 ── YouTube・OpenAI・Gemini・VOICEVOXのAPIキー取得"
---

# セットアップ Step 2 ── YouTube・OpenAI・Gemini・VOICEVOXのAPIキー取得

## 2-1. YouTube Data API v3のセットアップ

YouTubeへの動画アップロード・スケジュール公開を自動化するには、
YouTube Data API v3が必要です。

### Google Cloud Consoleでのプロジェクト作成

1. [console.cloud.google.com](https://console.cloud.google.com) にアクセス（Googleアカウントでログイン）
2. 画面上部のプロジェクト選択 → **[新しいプロジェクト]** をクリック
3. プロジェクト名を入力（例: `youtube-auto-channel`）→ **[作成]**

### YouTube Data API v3の有効化

1. 左メニュー → **[APIとサービス]** → **[ライブラリ]**
2. 検索ボックスに「YouTube Data API v3」と入力
3. 表示されたAPIをクリック → **[有効にする]**

### OAuth 2.0 クライアントIDの作成

1. **[APIとサービス]** → **[認証情報]** → **[認証情報を作成]** → **[OAuth クライアントID]**
2. アプリケーションの種類: **[デスクトップアプリ]** を選択
3. 名前を入力（例: `youtube-automation`）→ **[作成]**
4. **クライアントIDとクライアントシークレット** をメモ

### Refresh Tokenの取得

OAuth認証フローを一度実行して、長期有効なRefresh Tokenを取得します。
（詳細な手順は付録Aを参照）

取得したトークンをGitHub Repository Variablesに設定:

| 変数名 | 内容 |
|--------|------|
| `YOUTUBE_CLIENT_ID` | OAuth クライアントID |
| `YOUTUBE_CLIENT_SECRET` | OAuth クライアントシークレット |
| `YOUTUBE_REFRESH_TOKEN` | Refresh Token |

## 2-2. OpenAIのセットアップ（画像生成の主エンジン）

キャラクター画像・背景・図解・サムネイルなど、画像生成のすべての用途で
**gpt-image-2**（OpenAI）を主エンジンとして使います。
呼び出し自体は Gemini Image MCP サーバー経由のままですが、
MCP サーバーに渡す `provider` パラメーターで OpenAI のモデルを指定する構成です。
MCP サーバー名が歴史的に「gemini-image」のまま残っているだけで、
実体は OpenAI が主・Gemini がフォールバックという役割分担になっています（2026年7月時点）。

1. [platform.openai.com](https://platform.openai.com) にアクセス（OpenAIアカウントでログイン）
2. 左メニュー → **[API keys]**
3. **[Create new secret key]** をクリック
4. 作成されたシークレットキーをコピー（表示は一度きりなので必ず控える）

GitHub Repository Variablesに設定:

| 変数名 | 内容 |
|--------|------|
| `OPENAI_API_KEY` | OpenAI APIキー（画像生成の主エンジン。MCP サーバー未接続時の直接呼び出しフォールバックにも使用） |

:::message
OpenAIのAPIは従量課金です。無料枠はないため、請求上限（Hard limit）をOpenAI管理画面側で必ず設定してください。
上限に到達すると画像生成は自動的にGeminiへフォールバックする構成になっているため、
制作が完全に止まることはありませんが、キャラクターの見た目の一貫性にはわずかな影響が出る可能性があります。
:::

## 2-3. Geminiのセットアップ（画像生成のフォールバック用）

Geminiは、OpenAIの請求上限到達時に画像生成を止めないための **迂回路** として使います。
本書のシステムでは **Gemini Image MCP サーバー** の認証トークンとして使うため、
`GEMINI_MCP_AUTH_TOKEN` を設定します。

1. [aistudio.google.com](https://aistudio.google.com) にアクセス（Googleアカウントでログイン）
2. 左メニュー → **[Get API key]**
3. **[APIキーを作成]** をクリック
4. 作成されたAPIキーをコピー

GitHub Repository Variablesに設定:

| 変数名 | 内容 |
|--------|------|
| `GEMINI_MCP_AUTH_TOKEN` | Gemini Image MCP サーバー認証トークン（フォールバック時の画像生成に使用） |

:::message
Gemini APIには無料枠があります（2026年7月時点）。
主エンジンではなくなったため必須ではありませんが、OpenAIの請求上限到達時に制作を止めないための保険として設定しておくことを推奨します。
:::

## 2-4. VOICEVOXについて

**VOICEVOX** は音声合成ソフトです。重要なポイントがあります。

:::message
VOICEVOXはAPIキー不要・完全無料で使えます。
あなたのPCにインストールする必要もありません。
本書のシステムでは、Claudeのクラウド環境（コンテナ）内に
自動でインストール・起動されます（session-start.sh による自動セットアップ）。
:::

VOICEVOXの「利用規約」を必ず確認してください:
- キャラクターボイスの商業利用条件がキャラクターによって異なります
- YouTubeへの投稿・収益化を行う場合、該当キャラクターの規約を確認すること
- VOICEVOX 公式サイト: [voicevox.hiroshiba.jp](https://voicevox.hiroshiba.jp)

## 2-5. Slack通知のセットアップ（オプション）

進捗レポートをSlackで受け取りたい場合に設定します（任意）。

1. [api.slack.com/apps](https://api.slack.com/apps) で新しいアプリを作成
2. **Bot Token Scopes** に以下を追加:
   - `chat:write`（メッセージ送信）
   - `channels:join`（チャンネルへの参加）
3. アプリをワークスペースにインストール
4. **Bot User OAuth Token** をコピー

GitHub Repository Variablesに設定:

| 変数名 | 内容 |
|--------|------|
| `SLACK_BOT_TOKEN` | Bot User OAuth Token |
| `SLACK_CHANNEL_ID` | 通知を送るチャンネルのID |

:::message
Slackを使わない場合は設定不要です。通知なしで運用できます。
その場合、Claudeは各自動実行の結果をGitHub Issueのコメントに記録します。
:::

## セットアップ Step 2 チェックリスト

- [ ] Google Cloud Consoleでプロジェクトを作成した
- [ ] YouTube Data API v3を有効化した
- [ ] OAuth 2.0 クライアントIDを作成した
- [ ] Refresh Tokenを取得した
- [ ] YouTube関連の環境変数をGitHub Variablesに設定した
- [ ] OpenAI APIキーを取得・設定した（`OPENAI_API_KEY`）
- [ ] （推奨）Gemini APIキーを取得・設定した（`GEMINI_MCP_AUTH_TOKEN`・フォールバック用）
- [ ] （任意）Slack Botを作成・設定した
