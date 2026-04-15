---
title: "セットアップ Step 3 ── プロジェクト初期化とSKILL設定"
---

# セットアップ Step 3 ── プロジェクト初期化とSKILL設定

## 3-1. ディレクトリ構造の理解

本書のプロジェクトは以下のディレクトリ構造で管理します。
（主要なものだけ抜粋）

```
my-youtube-channel/          ← リポジトリのルート
├── CLAUDE.md                ← Claudeへの指示書（憲法）
├── docs/
│   ├── character-sheet.md   ← キャラクター設定
│   ├── rules/               ← 各種ルールファイル
│   │   ├── hourly-routing.md   ← 毎時タスクの時刻表
│   │   └── lessons.md          ← 繰り返しミス防止パターン
│   └── production-flow.md   ← 制作フロー全体の定義
├── .claude/
│   ├── skills/              ← Skillsが入るフォルダ
│   │   ├── script-pipeline/
│   │   │   └── SKILL.md
│   │   ├── audio-pipeline/
│   │   │   └── SKILL.md
│   │   └── ...
│   ├── hooks/               ← Hooksが入るフォルダ
│   │   ├── session-start.sh
│   │   └── post-compact.sh
│   └── rules/               ← 常時読み込みルールへのリンク
├── content/                 ← 生成されたコンテンツ
│   ├── scripts/             ← 台本JSONファイル
│   ├── meta/                ← 動画メタデータ
│   └── shorts/              ← Shorts用コンテンツ
├── assets/                  ← 画像・音声ファイル
│   ├── audio/               ← 生成された音声
│   └── images/              ← 生成された画像
└── tools/                   ← 自動化ツールスクリプト
    ├── youtube_scheduler.py
    ├── generate_audio.py
    └── ...
```

## 3-2. キャラクター設定の作成

本書のシステムでは、2体のキャラクターが会話形式で解説します。

キャラクター設定は `docs/character-sheet.md` に記述します。

```markdown
# キャラクター設定

## もっちー（ハムスター♂）
- 声: VOICEVOX 白上虎太郎
- 口調: 標準語・カジュアル
- 役割: ITオンチで、きなこから教わる生徒役
- 特徴: 投げ銭を積極的に求めたがる

## きなこ（セキセイインコ♀）
- 声: VOICEVOX 四国めたん
- 口調: 標準語・丁寧
- 役割: AIエージェントを使いこなす技術統括
- 特徴: 謙虚なバランサー、収益ウォッチ担当
```

:::message
キャラクターは独自のものに変更して構いません。自分のチャンネルに合ったキャラクターを設定してください。VOICEVOX のキャラクターを利用する場合は、各キャラクターの利用規約を必ず確認してください。
:::

## 3-3. Skillsの配置

本書のプロジェクトをテンプレートからコピーした場合、
Skillsはすでに `.claude/skills/` に配置されています。

自分で追加・カスタマイズする場合は、
`.claude/skills/{スキル名}/SKILL.md` を作成します。

## 3-4. session-start.shの設定

`.claude/hooks/session-start.sh` は、セッション開始時の環境設定スクリプトです。

主な設定内容:

```bash
#!/bin/bash
# タイムゾーン設定
export TZ=Asia/Tokyo

# GitHub認証（GH_TOKENが環境変数に設定されていればgh CLIが自動的に使用する）
export GH_TOKEN="$GH_TOKEN"

# VOICEVOXのインストール・起動（未起動の場合）
if ! curl -s http://localhost:50021/version > /dev/null 2>&1; then
    # VOICEVOXをダウンロードして起動
    ...
fi
```

このファイルはGitHubに保存されるため、
毎回のセッションで自動的に環境が整います。

## 3-5. 動作確認

セットアップが完了したら、Claude Codeのチャット画面で動作確認をします。

```
Claude Codeに以下を入力してみてください:
「git status を実行して、現在の状態を教えてください」
```

Claudeが実際のリポジトリの状態を教えてくれれば、
GitHubとの連携が成功しています。

## セットアップ Step 3 チェックリスト

- [ ] ディレクトリ構造を確認した
- [ ] キャラクター設定（character-sheet.md）を作成した
- [ ] `.claude/hooks/session-start.sh` を設定した
- [ ] Claude Codeでgit statusが動作することを確認した

セットアップはこれで完了です。
次の章から、実際のコンテンツ制作パイプラインを学んでいきます。
