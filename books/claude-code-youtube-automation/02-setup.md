---
title: "環境構築 — Claude Code + 必要ツールのセットアップ"
free: true
---

## このチャプターで学ぶこと

- 制作パイプラインに必要なツール一覧
- Claude Code のインストールと初期設定
- VOICEVOX Engine・Gemini API・YouTube Data API のセットアップ
- 環境変数の管理方法（クラウド環境 vs ローカル環境）

---

## 必要なツール一覧

| ツール | 用途 | 必須 |
|--------|------|------|
| **Claude Code** | 制作パイプラインの統合実行環境 | 必須 |
| **Node.js** (v20 LTS 以上) | Remotion、MCP サーバー | 必須 |
| **Python** (3.11 以上) | VOICEVOX 連携、YouTube API、各種スクリプト | 必須 |
| **Git** + **GitHub CLI** (`gh` v2.64+) | バージョン管理、PR 運用 | 必須 |
| **VOICEVOX Engine** | 音声合成 API サーバー | 必須 |
| **Gemini API** | 画像生成 | 必須 |
| **FFmpeg** | Remotion の動画レンダリングで内部的に使用 | 必須 |
| **YouTube Data API v3** | 動画アップロード・公開スケジュール管理 | Phase 6 以降 |
| **Docker**（オプション） | VOICEVOX Engine のコンテナ実行 | 推奨 |

---

## Claude Code のインストールと初期設定

```bash
npm install -g @anthropic-ai/claude-code
claude --version
```

:::message
**Anthropic のプランについて**: Scheduled Tasks（定期自動実行）を使用するには Claude Pro / Team / Enterprise / Max プランが必要です。ローカルでの手動実行であれば API キーがあれば利用可能です。
:::

プロジェクトディレクトリで初期化します。

```bash
cd your-project-directory
touch CLAUDE.md
mkdir -p .claude/{skills,rules,hooks}
```

`CLAUDE.md` はプロジェクト全体のルールブックです。Ch.04 で詳細に設計しますが、まず最低限の内容を記述しておきます。

```markdown
# プロジェクト概要

YouTubeチャンネル制作パイプライン。

## 実行環境

- VOICEVOX Engine: http://localhost:50021
- 言語: 日本語
```

---

## VOICEVOX Engine のセットアップ

### Docker で起動（推奨）

```bash
docker run --rm -p 50021:50021 voicevox/voicevox_engine:latest
```

### 動作確認

```bash
curl http://localhost:50021/version
# バージョン文字列が返れば正常
```

:::message alert
**音声生成パイプライン（Phase 4）実行時は、事前に VOICEVOX Engine が `localhost:50021` で起動している必要があります。**
:::

---

## Gemini API キーの取得と設定

1. [Google AI Studio](https://aistudio.google.com/) でAPIキーを生成
2. `.mcp.json` に MCP サーバー設定を記述

```json
{
  "mcpServers": {
    "gemini-image": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://your-gemini-mcp-server.workers.dev/mcp",
        "--header",
        "Authorization: Bearer ${GEMINI_MCP_AUTH_TOKEN}"
      ]
    }
  }
}
```

:::message
本書では Gemini API を MCP サーバー経由で呼び出します。MCP サーバー自体は Cloudflare Workers 上にデプロイします。詳細は本書のサンプルコードを参照してください。

**MCP サーバーの構築は上級トピックです。本書では Gemini API を直接呼び出す方法を推奨します。MCP サーバーの構築手順は Part 2（近日公開予定）で解説します。**
:::

---

## YouTube Data API の設定

1. [Google Cloud Console](https://console.cloud.google.com/) で **YouTube Data API v3** を有効化
2. **OAuth 2.0 クライアント ID**（デスクトップアプリ）を作成
3. スコープを追加:
   - `https://www.googleapis.com/auth/youtube.upload`
   - `https://www.googleapis.com/auth/youtube`
4. [OAuth 2.0 Playground](https://developers.google.com/oauthplayground/) でリフレッシュトークンを取得

:::message alert
**リフレッシュトークン・クライアントシークレットは絶対にコードやコミットメッセージに含めないでください。**
:::

:::message
**YouTube API プロキシについて**: `YOUTUBE_API_PROXY_URL` / `YOUTUBE_API_PROXY_AUTH_TOKEN` はクラウド環境（Claude Code Scheduled Tasks）でのみ必要です。ローカル環境では不要なため、スキップして構いません。
:::

---

## GitHub リポジトリの初期化

```bash
gh repo create your-channel-name --private --clone
cd your-channel-name

# ディレクトリ構成を作成
mkdir -p content/{research,scripts,meta}
mkdir -p assets/{audio,images,thumbnails}
mkdir -p output tools docs/rules remotion/src
mkdir -p .claude/{skills,rules,hooks}
```

構成のイメージです（完全版はリポジトリを参照）。

```
your-channel-name/
├── .claude/
│   ├── skills/     # Agent Skills
│   ├── rules/      # 自動読み込みされるルールファイル
│   └── hooks/      # PreToolUse / PostToolUse / Session フック
├── content/
│   ├── research/   # リサーチドキュメント
│   ├── scripts/    # 台本 JSON
│   └── meta/       # 公開メタデータ YAML
├── assets/
│   ├── audio/      # VOICEVOX 音声ファイル（WAV）
│   ├── images/     # 画像素材（PNG）
│   └── thumbnails/ # サムネイル画像
├── output/         # 完成動画（MP4）
├── tools/          # Python / シェルスクリプト
├── remotion/       # Remotion プロジェクト
├── .mcp.json       # MCP サーバー設定
└── CLAUDE.md       # プロジェクトのルールブック
```

### Git LFS の設定

```bash
git lfs install

cat << 'EOF' > .gitattributes
*.mp4 filter=lfs diff=lfs merge=lfs -text
*.png filter=lfs diff=lfs merge=lfs -text
# WAVはLFS対象外（クラウド環境でのプロキシ問題を回避）
assets/audio/**/*.wav !filter !diff !merge binary
EOF
```

:::message
クラウド環境（Scheduled Tasks）ではプロキシ経由で Git 操作するため、LFS Batch API が正常に動作しないケースがあります。WAV ファイルは LFS 対象外とすることを推奨します。
:::

---

## 環境変数の設定

### クラウド環境（Claude Code Scheduled Tasks）

セッション終了時にローカルファイルシステムが破棄されるため、 **`.env` や `.claude/settings.local.json` は使用できません**。

**設定場所**: `claude.ai` → スケジュールタスク設定 → 環境変数セクション（`.env` 形式で入力）

### ローカル環境

```bash
cat << 'EOF' > .env
SLACK_BOT_TOKEN=xoxb-your-token
GEMINI_API_KEY=your-gemini-api-key
YOUTUBE_CLIENT_ID=your-client-id
YOUTUBE_CLIENT_SECRET=your-client-secret
YOUTUBE_REFRESH_TOKEN=your-refresh-token
VOICEVOX_ENDPOINT=http://localhost:50021
EOF

echo ".env" >> .gitignore
echo ".claude/settings.local.json" >> .gitignore
```

### 環境変数一覧

| 変数名 | 用途 | 必要になる Phase |
|--------|------|----------------|
| `SLACK_BOT_TOKEN` | Slack 通知 | 全 Phase（オプション） |
| `GEMINI_API_KEY` | 画像生成 | Phase 4（画像） |
| `GEMINI_MCP_AUTH_TOKEN` | MCP サーバー認証 | Phase 4（画像） |
| `YOUTUBE_CLIENT_ID` | YouTube API 認証 | Phase 6 |
| `YOUTUBE_CLIENT_SECRET` | YouTube API 認証 | Phase 6 |
| `YOUTUBE_REFRESH_TOKEN` | YouTube API 認証 | Phase 6 |
| `YOUTUBE_API_PROXY_URL` | YouTube API プロキシ URL | Phase 6（クラウド環境のみ） |
| `YOUTUBE_API_PROXY_AUTH_TOKEN` | プロキシ認証トークン | Phase 6（クラウド環境のみ） |
| `VOICEVOX_ENDPOINT` | VOICEVOX 接続先 | Phase 4（音声） |

---

## 動作確認

各ツールのバージョンと疎通を確認します。

```bash
claude --version       # Claude Code
node --version         # v20.x.x 以上
python3 --version      # 3.11 以上
gh --version           # 2.64 以上
gh auth status         # 認証済みであること
curl -s http://localhost:50021/version  # VOICEVOX
ffmpeg -version        # FFmpeg
git lfs version        # Git LFS
```

---

## ハマりポイント

**VOICEVOX Engine が起動しない（Docker）**
: ポートマッピング `-p 50021:50021` を確認。別プロセスが 50021 を使用中でないか `lsof -i :50021` で確認。

**VOICEVOX の `audio_query` で日本語テキストが文字化けする**
: クエリパラメータとして渡すテキストは URL エンコードが必要です。Python では `urllib.parse.quote(text)` を使用してください。`requests` ライブラリを使う場合は `params={"text": text}` で自動エンコードされます。

**クラウド環境で環境変数が読み込まれない**
: `.claude/settings.local.json` は消えます。必ず claude.ai のスケジュールタスク設定で環境変数を管理してください。

**`gh pr edit --add-reviewer @copilot` でエラー**
: `gh --version` が v2.64 未満の場合に発生します。v2.88 以上を推奨します。

---

## まとめ

- **Claude Code**: `CLAUDE.md` と `.claude/` ディレクトリを初期化
- **VOICEVOX Engine**: Docker で `localhost:50021` に起動
- **Gemini API**: Google AI Studio で API キーを取得し、MCP サーバー設定を記述
- **YouTube Data API**: OAuth 2.0 の認証情報を取得
- **環境変数**: クラウド環境ではスケジュールタスク設定で管理

次のチャプターでは、Claude Code の基礎機能（Skills・Hooks・Agent Teams）について詳しく解説します。
