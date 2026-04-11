---
title: "トラブルシューティング ── よくある問題Q&A"
---

# トラブルシューティング ── よくある問題Q&A

## GitHub・セットアップ関連

### Q: GitHubにプッシュできない

**A**: 以下を順番に確認してください。

1. `GH_TOKEN` の環境変数が正しく設定されているか確認
   - GitHub → Settings → Developer settings → Personal access tokens
   - `repo` スコープが付与されているか確認
2. トークンの有効期限が切れていないか確認
3. Claude Codeのチャットで `gh auth status` を実行して認証状態を確認

### Q: Scheduled Tasksが実行されない

**A**: 以下を確認してください。

1. Claude Pro/Max プランに加入しているか
2. Scheduled Tasksの設定で「Active」になっているか
3. プロンプトの内容が正しいか（空のプロンプトは実行されない）

---

## API関連

### Q: YouTube APIエラー「invalid_grant」が出る

**A**: YouTube APIのリフレッシュトークンが期限切れです。

1. Google Cloud Console でOAuth認証フローを再実行
2. 新しい `YOUTUBE_REFRESH_TOKEN` を取得
3. GitHub Repository Variables を更新

:::message
この問題は本書の第7章（APIキーと環境変数）および第9章（セットアップ Step 2）で詳しく解説しています。
Claude Codeのチャットで「YouTube APIのinvalid_grantエラーの対処をしてください」と依頼すれば自動で診断します。
:::

### Q: Gemini APIで画像生成がエラーになる

**A**:

1. `GEMINI_API_KEY` の値が正しいか確認
2. Gemini APIの無料枠を超えていないか確認（Google AI Studioで確認）
3. 使用しているモデル名が最新か確認（モデル名は定期的に変更される）

---

## 音声・動画関連

### Q: VOICEVOXが起動しない

**A**: セッション開始時（session-start.sh）にVOICEVOXが自動インストールされますが、
ネットワーク環境によっては失敗することがあります。

Claude Codeのチャットで以下を依頼してください:
```
「VOICEVOXを手動で起動してください」
```

### Q: 音声がぎこちない（変な読み方をしている）

**A**: 発音辞書に登録されていない用語が含まれている可能性があります。

1. 問題のある音声のセリフを特定する
2. Claude Codeのチャットで以下を依頼:
   ```
   「V{ID}の{行番号}番のセリフ「{問題のテキスト}」の発音を修正してください」
   ```
3. Claudeが発音辞書に追記・音声を再生成します

### Q: 動画の尺が8分を下回っている

**A**: 台本のボリュームが不足しています。

Claude Codeのチャットで以下を依頼:
```
「V{ID}の台本を Phase 3からやり直して、15〜20分の尺になるよう追加コンテンツを生成してください」
```

---

## GitHub Issues関連

### Q: `status:waiting-user` のIssueが増えすぎている

**A**: Claudeがあなたの判断を待っている状態です。

- **緊急度「高」（`priority:high`）のものから対応**する
- 対応が難しいものは「今はスキップ」とIssueコメントに書いてCloseする
- Claude Codeのチャットで「status:waiting-userのIssueを整理してください」と依頼

### Q: 同じ動画のPRが複数作成されてしまった

**A**: マルチセッション（複数のClaude同時実行）による競合です。

1. 古い方のPRをCloseする（コメントに「重複のためClose」と記載）
2. 新しい方のPRを正とする

この問題の再発防止策は `docs/rules/session-concurrency-rules.md` に記載されています。

---

## よくある設定ミス

| 症状 | 原因 | 解決策 |
|------|------|--------|
| 音声ファイルが再生されない | パスの設定が二重になっている | `audio_file` のパスを `audio/V{ID}/...` 形式に修正 |
| 字幕が表示されない | `timed.json` の形式エラー | `audio-pipeline` を再実行 |
| SNS配信が実行されない | SNS系の環境変数が未設定 | GitHub Variables に各SNSのトークンを設定 |

---

## サポートを求める

本書の内容に関して困った場合は、Claude Codeのチャットに状況を説明すれば
診断・解決策の提案をしてくれます。

```
「{問題の症状}が発生しています。
エラーメッセージ: {エラー内容}
実行したコマンド: {コマンド}
解決策を教えてください」
```

Claudeは `docs/rules/lessons.md` の過去事例から類似問題を検索し、
対処法を提案します。

次の（最終）章では、本書のまとめとカスタマイズのヒントを紹介します。
