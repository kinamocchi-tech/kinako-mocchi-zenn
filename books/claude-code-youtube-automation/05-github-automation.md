---
title: "GitHub連携 — Issues, Milestones, Projects V2 の自動化"
---

## このチャプターで学ぶこと

- GitHub Issues + Milestones + Projects V2 による一元管理の設計
- Issue 命名規約とラベル運用ルール（特にステータスラベル）
- Video ID 採番ルール
- PR 運用ルール（ブランチ命名・コミットメッセージ・レビューフロー）
- `sync_project.py` と `project-manager` スキルによる自動化

---

## 設計思想

### 一元管理の原則

タスク管理は **GitHub 上で完結** させます。外部ツール（Notion、Trello 等）は使いません。

| リソース | 用途 |
|---------|------|
| **Issues** | 各タスクの詳細・議論・完了管理 |
| **Milestones** | M1〜M4 の進捗管理（完了率 % 表示） |
| **Projects V2** | Kanban ボードでステータス可視化 |
| **Labels** | タイプ・Phase・担当・優先度・ステータスで分類 |

### Issue は Claude Code が作成する

本プロジェクトでは、**Issue の大半を Claude Code が自動作成** します。

```
ユーザーの指示 / スケジュールタスク起動
  → Claude Code がマイルストーンへの反映可否を検討
  → 必要に応じて Issue を自動作成
  → Projects V2 に自動登録・ラベル設定
```

---

## Issue 命名規約

用途に応じて 3 つの命名パターンを使い分けます。

| パターン | 用途 | 例 |
|---------|------|-----|
| `[V{ID}] {Phase}: {概要}` | 動画単位のタスク | `[V007] Phase 3: 台本生成` |
| `T{M}-{N}: {タスク名}` | マイルストーン由来のタスク | `T3-1: パイロット動画制作` |
| `{type}: {概要}` | 開発系タスク | `feat: 字幕均等分割対応` |

---

## ラベル運用ルール

### ラベル体系

| プレフィックス | 用途 | 例 |
|-------------|------|-----|
| `type:` | タスクの種類 | `type:content`, `type:feature` |
| `phase:` | 制作 Phase | `phase:2-research`, `phase:3-script` |
| `assignee:` | 担当者 | `assignee:claude`, `assignee:user` |
| `priority:` | 優先度 | `priority:high`, `priority:medium` |
| `status:` | アクション待ち状態 | `status:waiting-user` |

### ステータスラベルの設計

**ユーザーが対応すべき Issue を一目で判別できる** ことが最大の目的です。

| ラベル | 色 | 用途 |
|--------|------|------|
| `status:waiting-user` | 黄 | ユーザーのアクション待ち（Deep Research 実行依頼など） |
| `status:waiting-claude` | 緑 | Claude Code の作業待ち |
| `status:in-progress` | 青 | 作業中 |
| `status:blocked` | 赤 | 外部要因でブロック |

**運用ルール**:
- Issue 作成時に適切な `status:` ラベルを付与する
- ステータスが変わったら即座に更新する（古いラベルは除去）
- **ネタ候補（`phase:1-neta`）には `status:` ラベルを付与しない**（バックログに表示すべきでない）

:::message
ユーザーは `status:waiting-user` でフィルタするだけで、自分がやるべきことの一覧を確認できます。
:::

---

## Video ID 採番ルール

動画は `V001`、`V002`... の連番で管理します。

```bash
# 最大 Video ID の確認コマンド
gh issue list -R your-repo/your-channel \
  --search "[V" --state all --limit 1000 \
  --json title \
  --jq '[.[] | .title |
    (try capture("\\[V(?<n>[0-9]+)\\]") catch empty) |
    .n // empty | tonumber] | max // 0'
```

このコマンドで全 Issue タイトルから `[V{数字}]` パターンを検索し、最大番号 + 1 を次の Video ID とします。

- **形式**: `V` + 3 桁ゼロパディング（`V004`, `V005`）
- **権威ソース**: Issue タイトルの `[V{ID}]` パターン（Projects V2 フィールドより優先）
- **ギャップ禁止**: 番号を飛ばさない

:::message alert
Projects V2 の単一選択フィールドに新しいオプションを API で追加する方法は、2026 年 3 月時点で存在しません。V007 以降の Video ID オプションは GitHub UI から手動追加するか、Issue タイトルベースの検出で運用します。
:::

---

## Projects V2 の設計

### カスタムフィールドと主要ビュー

カスタムフィールド（Status、Phase、Video ID 等）は GitHub の Projects 設定画面から手動で作成します。フィールド作成後に `sync_project.py` が自動同期を担います。

| フィールド | 選択肢 |
|-----------|--------|
| **Status** | Backlog / Todo / In Progress / In Review / Done |
| **Phase** | Setup / Phase 1〜7 / Launch |
| **Video ID** | V001, V002, ... |

最重要ビューは **「ユーザー To-Do」** です。フィルタ設定:

```
assignee-type:"user","both" -status:Done -status:Backlog
```

---

## PR 運用ルール

### ブランチ命名規則

| プレフィックス | 用途 | 例 |
|-------------|------|-----|
| `content/V{ID}-{テーマ}` | 動画単位のコンテンツ | `content/V007-anthropic` |
| `claude/{動画ID}-{工程}-{セッションID}` | 自動パイプライン | `claude/V007-audio-01Qddb8` |
| `feat/{機能名}` | ツール開発 | `feat/subtitle-splitter` |
| `fix/{修正名}` | バグ修正 | `fix/pronunciation-dict` |

:::message
`main` への直接 push は禁止です。`pre-git-push-check.sh` フックが物理的にブロックします。全ての変更は PR 経由でマージします。
:::

### コミットメッセージ規約

```
[V{動画ID}] {Phase名}: {概要}
```

例:
```
[V007] research: Anthropicリサーチ完了
[V007] script: 台本v1生成
[V007] audio: VOICEVOX音声生成完了（142セリフ・15.3分）
```

### PR レビューフロー

```
実装完了
  → セルフレビュー（Agent Teams で並列レビュー）
  → PR 作成（自律実行・ユーザー承認不要）
  → Slack で PR 作成を通知
  → AI レビュー依頼（Gemini Code Assist + GitHub Copilot）
  → 自動監視（subscribe_pr_activity によるイベント駆動。詳細は Ch.14 参照）
  → 指摘対応 / 問題なし判定
  → 自動マージ（squash）
  → 完了報告（Slack 通知）
```

**AI レビュアー**:

| レビュアー | 依頼方法 |
|-----------|---------|
| Gemini Code Assist | PR コメントで `/gemini review` |
| GitHub Copilot | `gh pr edit {number} --add-reviewer @copilot -R your-repo` |

AI レビューの全指摘を解消したら、ユーザー確認なしで自動マージします。サーキットブレーカー（修正サイクル 2 回上限）が発動した場合のみ、ユーザーに報告して判断を仰ぎます。

---

## 自動化の実装

### sync_project.py — Projects V2 同期ツール

`tools/sync_project.py` は以下を自動化します（詳細はリポジトリを参照）。

1. Phase 2 Issue への Video ID 自動採番
2. ネタ候補 Issue への不適切な `status:waiting-user` ラベル除去
3. 全オープン Issue の Projects V2 登録
4. `status:` ラベルに連動した `Assignee Type` 自動設定

```python
# status: ラベル → Assignee Type マッピング
STATUS_TO_ASSIGNEE = {
    "status:waiting-user": OPT_ASSIGNEE_USER,
    "status:waiting-claude": OPT_ASSIGNEE_CLAUDE,
    "status:in-progress": OPT_ASSIGNEE_CLAUDE,
    "status:blocked": OPT_ASSIGNEE_USER,
}
```

### ネタ候補の自動昇格フロー

`/refinement` スキルがスコア 15 点以上のネタ候補を自動検出し、制作 Issue に昇格させます。

```
1. スコア ≥ 15 のネタ候補を検出
2. 次の Video ID を採番（連番）
3. [V{ID}] Phase 2: Deep Research実行依頼 Issue を自動作成
4. Projects V2 に登録・ラベル設定
5. 元のネタ候補 Issue をクローズ
```

### 自動化フロー全体図

```
スケジュールタスク（毎時）
  ↓
/project-sync スキル → sync_project.py 実行
  ├── Video ID 未採番の Phase 2 Issue にタイトル更新
  ├── 全オープン Issue を Projects V2 に登録
  └── status: ラベルに連動して Assignee Type を設定
  ↓
ユーザーは「ユーザー To-Do」ビューで自分のタスクを確認
```

---

## ハマりポイント

**`gh issue list` のデフォルト件数**
: デフォルトは 30 件です。Issue が 100 件を超えるプロジェクトでは `--limit 1000` を明示的に指定してください。

**プロキシ環境での gh CLI**
: クラウド環境ではリポジトリやブランチが自動検出できません。`gh pr create` には必ず `--head` と `--base` と `-R` を明示します。

```bash
gh pr create \
  --head claude/V007-audio-01Qddb8 \
  --base main \
  -R your-repo/your-channel \
  --title "[V007] audio: VOICEVOX音声生成完了"
```

**Projects V2 は GraphQL API**
: Projects V2 の操作は REST API ではなく GraphQL API を使います。`sync_project.py` では `urllib.request` で直接 GraphQL クエリを発行しています。

---

## まとめ

| 機能 | 自動化内容 |
|------|----------|
| Issue 作成 | Phase 完了時に次 Phase の Issue を自動作成 |
| ラベル管理 | `status:` ラベルでアクション待ち状態を可視化 |
| Video ID 採番 | Issue タイトルから自動検出・連番付与 |
| Projects V2 同期 | `sync_project.py` で全 Issue を自動登録・フィールド設定 |
| PR レビュー | AI レビュー → 自動監視 → 指摘対応 → 自動マージ |

次のチャプターからは Part 2（制作パイプライン）に入り、テーマ発見の自動化から解説を始めます。ここまでで構築した基盤（Skills, Hooks, Agent Teams, CLAUDE.md, GitHub 連携）が、制作の各工程でどのように活用されるかを見ていきましょう。
