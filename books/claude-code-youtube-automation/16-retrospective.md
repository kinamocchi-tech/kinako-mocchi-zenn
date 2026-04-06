---
title: "レトロスペクティブ — KPT + Try Issue 自動化"
---

## このチャプターで学ぶこと

- KPT フレームワークをパイプラインに組み込む動機と設計思想
- 3つの専門レビュアーを Agent Teams で並列実行するアーキテクチャ
- Try アイテムを GitHub Issue として自動生成・管理するフロー
- `retro-try-handler` による週次自動対応のしくみ

## 背景 — 「次回気をつける」が消えていく問題

AI 駆動のパイプラインが持つ最大のリスクのひとつは、**問題の原因がセッションをまたいで引き継がれない**ことです。Claude Code は毎セッション新しい状態から始まるため、改善を永続させるにはコードやドキュメントに「焼き付ける」必要があります。

```text
従来: パイプライン実行 → 問題発生 → 修正 → セッション終了 → 繰り返し

改善後: パイプライン実行 → PR マージ → レトロスペクティブ自動実行
          → KPT 生成 → Try を GitHub Issue 化 → 改善が累積
```

## 設計思想

### 3役割並列レビュー

レトロスペクティブを単一エージェントに任せると視点が偏ります。本プロジェクトでは3つのレビュアーを **Agent Teams（並列サブエージェント）** として同時起動します。並列実行により逐次実行と比べて所要時間を約3分の1に短縮できます。

| 役割 | 担当範囲 | 主な評価観点 |
|------|---------|------------|
| **コンテンツ品質レビュアー** | 台本・音声・画像の品質 | fact_check_flags 解消率、キャラクター設定の遵守、尺目標達成状況 |
| **プロセス・自動化レビュアー** | ワークフロー効率 | 手動介入の頻度、ボトルネック、スキップ可能なステップ |
| **技術・ツールレビュアー** | コード・ドキュメントの整合性 | エラーパターン、ドキュメントと実装の乖離、バリデーション追加候補 |

### Try の即時 Issue 化

KPT を実施しても Try が「メモ」で終わると実行されません。Try を作成した瞬間に GitHub Issue として登録し、次のセッションで Claude Code が自動的に参照・対応できるようにします。

## 実装詳細

### レトロスペクティブ実行フロー

```text
Step 0: コンテキスト収集（git log, PR情報, 品質メトリクスを取得）
Step 1: Agent Teams 起動（3役割を Haiku で並列実行）
Step 2: KPT 結果のマージ（重複する Try を1アイテムに集約）
Step 3: Try アイテムを GitHub Issue 化（優先度 high → medium → low 順）
Step 4: Slack 通知（KPT サマリーを送信）
Step 5: 完了報告
```

### KPT の出力フォーマット

各サブエージェントは以下の JSON 形式で結果を返します。

```json
{
  "role": "quality",
  "pipeline": "script",
  "video_id": "V007",
  "keep": [
    { "title": "fact_check_flags の自動検出が機能した", "detail": "..." }
  ],
  "problem": [
    { "title": "emotion フィールドに無効値が混入した", "detail": "..." }
  ],
  "try": [
    {
      "title": "emotion フィールドの有効値リストをバリデーションに追加する",
      "detail": "post-tool-use-validate.sh に emotion の許容値チェックを追加する",
      "priority": "high",
      "assignee": "claude",
      "estimated_effort": "small"
    }
  ]
}
```

### Try アイテムの Issue 化

**Issue タイトル命名規則:**

```text
[Retro][{pipeline}] {Try内容の要約}

例:
[Retro][script] emotion フィールドの有効値リストをバリデーションに追加する
[Retro][audio] 発音辞書カバレッジチェックを音声生成前に必ず実行する
```

**ラベル体系:**

| ラベル | 付与条件 |
|--------|---------|
| `type:retro-try` | **全 Try Issue に必須**（フィルタ用の主キー） |
| `assignee:claude` / `assignee:user` | 担当者に応じて |
| `priority:high` / `medium` / `low` | 優先度に応じて |
| `status:waiting-claude` / `status:waiting-user` | 担当者に応じて |

```bash
# 未対応の Try Issue を一覧取得
gh issue list -R {owner}/{repo} --label "type:retro-try" --state open --limit 1000
```

### retro-try-handler による週次自動対応

`type:retro-try` かつ `assignee:claude` の Issue は、毎週月曜 07:00 に `retro-try-handler` スキルが自動対応します。

対応可能な典型的な Try の例:
- `post-tool-use-validate.sh` に新しいバリデーションチェックを追加する
- `CLAUDE.md` にルールを追記する
- `.claude/skills/` の SKILL.md を更新する

設計の根本的な変更や外部サービスの設定が必要なものは `assignee:user` として登録し、ユーザーの判断を促します。

## 実装例 — Try Issue の自動生成

以下は `retrospective` スキルが生成する Try Issue の実例です。

**Issue タイトル**: `[Retro][script] emotion フィールドの有効値リストをバリデーションに追加する`

**Issue 本文**:

````markdown
## 背景

V007 の台本 PR で、emotion フィールドに `angry` という無効値が混入し、
Gemini Code Assist から指摘を受けた（PR #221）。

## Problem

emotion フィールドの有効値チェックが Lv2（セルフレビュー）にしか
存在しないため、PR 作成前に見逃されるケースがある。

## Try（提案する対策）

`post-tool-use-validate.sh`（Lv3 フック）に emotion の有効値チェックを追加する。

有効値: normal / neutral / excited / confused / sad / whisper / tsukkomi / teaching / gentle

```bash
invalid_emotions=$(echo "$lines_json" | jq -r '
  [.[] | select(.emotion != null) |
   select(.emotion | IN("normal","neutral","excited","confused",
                        "sad","whisper","tsukkomi","teaching","gentle") | not)] |
  if length > 0 then
    (.[0:3] | map("  id=\(.id): emotion=\(.emotion)") | join("\n"))
  else empty end
' 2>/dev/null || true)

if [ -n "$invalid_emotions" ]; then
  jq -n --arg m "$invalid_emotions" \
    '{"systemMessage": "[script-validator] emotion 無効値: \($m)"}'
  exit 2
fi
```

## 完了条件

- [ ] `post-tool-use-validate.sh` に上記チェックを追加
- [ ] V001 の台本 JSON で動作確認
- [ ] CLAUDE.md の「ハーネスエンジニアリング」表を Lv3 に更新
````

このような具体的なコードスニペット付きの Issue が自動生成されることで、`retro-try-handler` が月曜 07:00 に即座に対応できます。

## ハマりポイント

### 3役割の結果に重複が多い

同じ問題を3役割がそれぞれ Try として挙げることがあります。Step 2（KPT 結果のマージ）でタイトルの類似度が高いものをグループ化し、最も詳細な `detail` を持つアイテムを代表として選択します。

### レトロスペクティブ自体が重くなる

パイプラインが積み上がると、コンテキスト収集で取得する情報が膨大になります。解決策は2つです。収集する情報を直近のパイプライン実行分のみに限定すること（`git log --since="24 hours ago"` など）と、各サブエージェントが返す KPT を 1,000〜2,000 トークンのサマリーに制限することです。

:::message alert
レトロスペクティブ自体がボトルネックになってはいけません。目安は5〜10分以内で完了すること。それ以上かかる場合はコンテキスト収集の範囲を絞ってください。
:::

### lessons.md の肥大化

`docs/rules/lessons.md` は全セッションで自動読み込みされるため、エントリが増えすぎるとトークン消費が増加します。本プロジェクトでは **50エントリ超で肥大化警告 Issue を自動生成** し、古いエントリを `docs/rules/lessons-archive.md` に移動する仕組みを設けています。

昇格・アーカイブの基準:

| 状態 | 条件 | 操作 |
|------|------|------|
| **昇格** | SKILL.md / docs/rules / CLAUDE.md に反映済み | `昇格先:` フィールドを設定 |
| **アーカイブ** | 昇格済み かつ 60日以上経過 | `lessons-archive.md` に移動 |

アーカイブ操作は `retro-try-handler` の Step 5.5 で自動実行されるため、手動作業は不要です。

## まとめ

- **KPT フレームワーク** で問題を構造的に捉え
- **Agent Teams 3役割** で多角的な視点から評価し
- **Try の即時 Issue 化** で改善を永続させ
- **retro-try-handler** で週次自動対応を実現する

この仕組みがあることで、パイプラインは動かすたびに賢くなります。初期の動画制作では繰り返し発生していた `emotion` フィールドの無効値問題は、レトロスペクティブが3回ほど回ったタイミングで自動バリデーションに組み込まれ、それ以降は一度も発生しなくなりました。

次章では、本書全体を振り返り、AI 駆動コンテンツ制作の可能性と限界、今後の展望を解説します。
