---
title: "SkillsとHooksとは ── タスク分割と自動トリガー"
---

# SkillsとHooksとは ── タスク分割と自動トリガー

## Skillsとは

**Skills（スキル）** とは、Claude Codeに特定の作業手順を覚えさせる **「マニュアルファイル」** です。

例えば、「台本を生成する手順」を `script-pipeline/SKILL.md` というファイルに詳細に記述しておくと、
Claudeは `/script-pipeline` と呼び出すだけで、そのマニュアルに従って台本を自動生成します。

料理で例えると、レシピカードを作っておくと誰でも同じ料理が作れるのと同じです。
Skillsは **「Claudeのためのレシピカード」** です。

## Skillsの構成

本書のプロジェクトには以下のようなSkillsがあります。

| スキル名 | 役割 |
|---------|------|
| `script-pipeline` | 台本の自動生成（Phase 3） |
| `audio-pipeline` | 音声の自動合成（Phase 4A） |
| `image-pipeline` | 画像の自動生成（Phase 4B） |
| `video-pipeline` | 動画の自動制作（Phase 5） |
| `theme-discovery` | ネタ候補の自動収集（Phase 1） |
| `self-reviewer` | 品質の自動チェック |
| `retrospective` | 振り返り・改善点の自動記録 |

各Skillは `.claude/skills/{スキル名}/SKILL.md` というファイルに定義されています。

## SKILL.mdの中身

SKILL.mdには、そのSkillが実行すべき手順が詳細に書かれています。

```markdown
# script-pipeline SKILL.md

## 概要
台本生成パイプラインを自動実行する

## 前提条件
- Phase 2（リサーチ）が完了していること
- content/research/V{ID}_research.md が存在すること

## ステップ
### Step 1: リサーチ確認
  対象動画のリサーチドキュメントを読み込む

### Step 2: キャラクター設定確認
  docs/character-sheet.md を読み込む

### Step 3: 台本生成
  リサーチとキャラクター設定に基づいて台本JSONを生成する
  目標尺: 15〜20分（1分≒400文字）

...（詳細な手順が続く）
```

## Hooksとは

**Hooks（フック）** とは、**特定のタイミングで自動実行されるスクリプト** です。

「フック」は「引っかける」という意味で、
「ある出来事が起きたとき（フック）に、自動で何かを実行する」仕組みです。

## 本書で使う主なHooks

| フック名 | 実行タイミング | 何をするか |
|---------|-------------|---------|
| `session-start.sh` | セッション開始時 | VOICEVOXのインストール・起動、認証情報の設定 |
| `post-compact.sh` | コンテキスト圧縮時 | 未保存の作業を自動でGitHubに保存 |
| `post-tool-use-validate.sh` | ファイル保存後 | 台本JSONの文法・ルール違反を自動チェック |

## session-start.sh の働き

`session-start.sh` は、Scheduled Tasksで毎時Claudeが起動するたびに実行されます。

このファイルには以下の処理が書かれています：

```bash
# タイムゾーンをJST（日本時間）に設定
export TZ=Asia/Tokyo

# VOICEVOXをダウンロード・起動（音声合成のため）
if ! curl -s http://localhost:50021/version > /dev/null 2>&1; then
    # VOICEVOX未起動なら起動する
    ./run_voicevox.sh &
fi

# GitHubへの認証情報を設定（GH_TOKENが環境変数に設定済みなので、gh CLIは自動的に使用する）
export GH_TOKEN="$GH_TOKEN"
```

これにより、Claudeが起動するたびに「音声合成できる環境」が自動で整います。
あなたが手動で設定する必要はありません。

## SkillsとHooksの違い

| 項目 | Skills | Hooks |
|------|--------|-------|
| 実行タイミング | Claudeが呼び出したとき（能動的） | 特定のイベント発生時（受動的・自動） |
| 定義場所 | `.claude/skills/*/SKILL.md` | `.claude/hooks/*.sh` |
| 主な用途 | 作業手順のガイド | 環境準備・バリデーション |

:::message
「Skillsは作業レシピ、Hooksは自動アラーム」と覚えると理解しやすいです。
:::

## スラッシュコマンド（/コマンド名）の仕組み

Claudeに「`/script-pipeline`」と入力すると、
対応するSkillの `SKILL.md` が自動で読み込まれ、書かれた手順に従って作業が実行されます。

本書のScheduled Tasksでは、Claudeが時刻に応じて自動で適切なスラッシュコマンドを呼び出します。

```
06:00 に起動したClaude:
  → CLAUDE.md を読む
  → 「06:00はscript-pipelineを実行する」というルールを確認
  → /script-pipeline を自動実行
```

あなたがスラッシュコマンドを直接打つ必要はありません。Claudeが判断して自動実行します。

## Hooksの具体例: 台本バリデーション

`post-tool-use-validate.sh`（台本ファイル保存時に自動実行）は以下をチェックします。

- 台本のJSON形式が正しいか
- キャラクターが方言を喋っていないか（もっちーが京都弁を使ってないか等）
- 数値を含む発言にファクトチェックフラグが付いているか

重大なルール違反（JSON形式エラー・方言使用など）の台本は **保存がブロックされ**、軽微な違反は警告として通知されます。これにより品質を自動で担保できます。

次の章では、各種サービスと連携するために必要な **APIキーと環境変数** について学びます。
