---
title: "Phase 4A 音声生成 ── VOICEVOXがクラウドで動く理由"
---

# Phase 4A 音声生成 ── VOICEVOXがクラウドで動く理由

## このフェーズでやること

Phase 4Aでは、台本JSONの各セリフを **VOICEVOX（音声合成エンジン）** で音声化します。

実行タイミング: **毎日 10:00 JST**（自動実行）

## VOICEVOXとは

**VOICEVOX** は、日本語に特化した高品質な無料音声合成ソフトです。
複数のキャラクターボイスを持ち、感情表現や話速も調整できます。

本書では:
- **もっちー** → 白上虎太郎（VOICEVOX）
- **きなこ** → 四国めたん（VOICEVOX）

を使用しています。

:::message
VOICEVOXは「`localhost:50021`」（あなたのコンピューターの特定ポート）で動作します。
本書のシステムでは、これが **Claudeのクラウドコンテナ内の localhost** であることがポイントです。
:::

## 「クラウドでlocalhost？」という疑問に答える

「localhostって自分のPCのことじゃないの？」と思った方へ。

**正解です** — localhost は通常、自分のPCを指します。
ただし本書のシステムでは、Claude Codeが **Claudeのクラウドコンテナ（専用のLinuxサーバー）** 上で動作します。

そのコンテナ（サーバー）の中でVOICEVOXが起動するため、
コンテナの視点では「localhost:50021」にVOICEVOXが動いています。

```
あなたのPC  ←→  インターネット  ←→  Claudeのクラウドコンテナ
                                         └── VOICEVOX（localhost:50021）
                                         └── Remotion
                                         └── Python スクリプト
```

あなたのPCに何もインストールせずに、クラウドで音声が生成されます。

## session-start.sh でVOICEVOXが自動起動する仕組み

セッション開始時に `session-start.sh` が実行され、以下の処理が行われます。

1. VOICEVOX がまだ起動していなければ、クラウドコンテナにダウンロード
2. VOICEVOXを起動（バックグラウンドで動作開始）
3. 起動完了を確認してから処理を続行

この処理に約15〜30秒かかりますが、自動です。

## 音声生成の流れ

`audio-pipeline` スキルは以下の処理を実行します。

```
台本JSON
  ↓
発音辞書の適用（英語用語をカタカナに変換）
  例: "Claude Code" → "クロードコード"
  ↓
VOICEVOX APIに送信
  ↓
WAVファイルとして保存（assets/audio/V{ID}/001.wav など）
  ↓
全セリフ分を繰り返す
```

## 発音辞書の重要性

英語の技術用語をそのままVOICEVOXに渡すと、
ぎこちない発音になることがあります。

本書では `docs/pronunciation-dictionary.json` に **発音辞書** を用意し、
英語用語→カタカナの読みに変換してから音声生成しています。

```json
{
  "english": [
    {"pattern": "Claude Code", "reading": "クロードコード"},
    {"pattern": "GitHub", "reading": "ギットハブ"},
    {"pattern": "Gemini", "reading": "ジェミナイ"}
  ]
}
```

新しい技術用語が登場したら、辞書に追加することで品質を維持できます。

## 音声ファイルの保存場所

生成された音声ファイルは以下に保存されます:

```
assets/audio/V{動画ID}/{行番号}.wav
例: assets/audio/V005/001.wav, 002.wav, ...
```

次の章では、シーンに合った **キャラクター画像が自動生成される仕組み（Phase 4B）** を解説します。
