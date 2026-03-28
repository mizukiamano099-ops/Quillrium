# Quill-rium（クイルリウム）β

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Beta](https://img.shields.io/badge/status-beta-blue)
![Powered by Claude Code](https://img.shields.io/badge/Powered%20by-Claude%20Code-blueviolet)

> **「短編を、最後まで書ける」**

Claude Code で動く、短編小説執筆支援フレームワーク。
インタビューから始まり、シーン執筆・評価・再レンダリングまでをサポートします。

[English README](README.en.md)

---

## Quick Start

### 必要なもの

- [Claude Code](https://claude.ai/code) がインストール済みであること

### 1. リポジトリを取得する

```bash
git clone https://github.com/mizukiamano099-ops/Quillrium
cd Quillrium
```

### 2. Claude Code を起動する

```bash
claude
```

### 3. 話しかける

```
新しい小説を書きたい
```

インタビューが始まります。タイトル・あらすじ・キャラクター・構成を一緒に設計して、そのままシーン執筆に入れます。

---

## 基本フロー

```
話しかける
    ↓
PHASE 1：インタビュー
  タイトル / ジャンル / あらすじ / キャラクター / 構成 / ボリューム
    ↓
PHASE 2：シーン執筆
  おたすけ提案（3択）→ ユーザーが選ぶ → Claude が書く → バケツマン評価
    ↓
  （全シーン完了）
    ↓
PHASE 4：Opus 再レンダリング（任意）
  Sonnet 草稿を確認 → Opus で一括書き直し → 品質アップ
```

各シーンは `Story/{作品タイトル}/scenes/scene_N.md` に自動保存されます。
`git commit & push` まで自動で行います。

---

## 機能リファレンス

### ボリュームゾーン

文字数ではなく、読み応えの感覚でボリュームを指定します。
「だいたい〇〇字くらい」と伝えると、自動でゾーンに変換して確認を取ります。

| ゾーン | 目安 | シーン数 |
|---|---|---|
| 掌編 | ひと読みで完結 | 1〜2 |
| 短編 | 読切として満足感がある | 3〜5 |
| 中編 | 読み応えのある読切 | 6〜10 |
| 短編連載 | 各話完結型の連作 | 話数は後で決める |

---

### フェーズ一覧

| フェーズ | 内容 | 起動タイミング |
|---|---|---|
| PHASE 1 | インタビュー・構成設計 | `新しい小説を書きたい` |
| PHASE 2 | シーン執筆 | `シーンNを書いて` |
| PHASE 3 | プロット出力（手書き用） | `プロットを出して` |
| PHASE 4 | Opus 一括再レンダリング | `再レンダリングして` |

---

### おたすけモード

シーン執筆前に、毎回3つの方向性を提案します。

```
A：流れ重視  ── アウトラインの目的を最短で達成する正道
B：矛盾重視  ── キャラクターの wants/but が衝突・露呈する角度
C：感情重視  ── 山場に向けてリスクをとる選択
```

選ぶか、「こういう感じにしたい」と伝えるだけで書き始めます。
「おたすけOFF」と言うとセッション中は提案を止めます。

---

### バケツマン評価

シーン完了後、EVAL_CHAR（デフォルト：バケツマン）がキャラの口調で批評します。

```
「このFG、自分の感情に気づいてない。でも全部バレてる」

★ キャラ一貫性：★★★
★ 山場の機能 ：★★★
★ 読みやすさ ：★★☆

→ 通学路の場面、もう少し短くできる
```

評価担当は QUILL_STATE の `EVAL_CHAR` フィールドで変更できます。
作品のキャラを担当にすると「自分が作ったキャラが自分の物語を批評する」体験になります。

---

### Sonnet 草稿 → Opus 再レンダリング

品質を重視するときは、このフローを使います。

```
Sonnet で全シーン草稿（速く・安く構造を検証）
    ↓
気に入ったら Opus に切り替えて PHASE 4 を実行
    ↓
草稿は scene_N_draft.md として残る（比較・差し戻し可能）
```

インタビュー完了時と全シーン完了時に、Claude からOpus切り替えの提案が出ます。

---

### ディレクトリ構成

```
Quill-rium/
├── CLAUDE.md              ← Claude Code への指示（編集可）
├── engines/               ← エンジン定義（編集しない）
├── characters/
│   └── eval_cast/         ← 評価担当キャラ（共通）
├── templates/             ← 雛形（編集しない）
├── samples/               ← チュートリアル用サンプル
└── Story/
    └── {作品タイトル}/    ← 作品ごとに自動生成
        ├── state/
        │   └── current.md ← QUILL_STATE（自動管理）
        ├── scenes/
        ├── characters/
        │   └── main_cast/
        └── plots/
```

---

## βについて

現在 **β版** です。動作確認・フィードバックを歓迎します。

- フィードバック → [Issues](https://github.com/mizukiamano099-ops/Quillrium/issues)
- 既知の制限：サンプル作品は `samples/osananajimi_bucket/` を参照してください

---

*Quill-rium β — Powered by Claude Code*
