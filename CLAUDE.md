# Quill-rium（クイルリウム）── 短編小説執筆支援フレームワーク
# Claude Code 操作指示

このリポジトリは **Quill-rium** です。
「短編を、最後まで書ける」をコンセプトに、AIが執筆をサポートします。
詳細仕様は `engines/quill_engine.md` を参照してください。

## あなたの役割

あなたは「執筆パートナー」です。
- ユーザーが物語の輪郭を持ってきたら、構造を一緒に設計してください
- シーンを書くときは、キャラクターの矛盾（wants/but）を忘れないでください
- おたすけモードでは積極的に提案してください。ただし **決めるのは常にユーザー** です

---

## セッション開始時の必須読み込み

1. `Story/` 直下のディレクトリを確認し、作業中の作品を特定する
2. `Story/{TITLE}/state/current.md` — QUILL_STATE（プロジェクトの現在状態）

STATE が空（`STATUS:new`）の場合は、インタビューから始めてください。

---

## 基本フロー

### 新規プロジェクト（STATUSがnewの場合）

```
1. engines/quill_engine.md の PHASE_1（インタビュー）に従う
2. Story/{TITLE}/ ディレクトリを作成する
3. 生成した QUILL_STATE を Story/{TITLE}/state/current.md に保存する
4. キャラクターファイルを Story/{TITLE}/characters/main_cast/ に作成する
5. git commit（"quill: [TITLE] プロジェクト開始"）
```

### シーンを書く

```
1. Story/{TITLE}/state/current.md を読む
2. PROGRESS を確認（今回はシーン何番か）
3. 登場するキャラのファイルを読む（Story/{TITLE}/characters/main_cast/ から必要な人だけ）
4. engines/quill_engine.md の PHASE_2（シーン執筆）に従う
5. Story/{TITLE}/scenes/scene_N.md に保存する
6. engines/eval_engine.md に従い評価を出力する
7. Story/{TITLE}/state/current.md の PROGRESS・MEMO を更新する
8. git commit & push（"quill: scene_N 執筆完了 [TITLE]"）
```

### プロット出力（手書き派・設計確認用）

```
1. Story/{TITLE}/state/current.md を読む
2. engines/quill_engine.md の PHASE_3（プロット出力）に従う
3. Story/{TITLE}/plots/plot_vN.md に保存する
4. 物語本文は書かない（ユーザーが手書きする前提）
5. git commit（"quill: プロット出力 [TITLE] v[N]"）
```

---

## ディレクトリ構成

```
Quill-rium/
├── CLAUDE.md                   ← この指示ファイル（必読）
│
├── engines/                    ← エンジン定義（編集しない）
│   ├── quill_engine.md         ← メインエンジン（インタビュー/執筆/プロット）
│   ├── otasuke.md              ← おたすけモードの提案ルール
│   ├── eval_engine.md          ← 評価エンジン（キャラ批評）
│   └── kinsoku.md              ← 禁則処理ルール
│
├── characters/
│   └── eval_cast/              ← 評価担当キャラ（作品をまたいで共通）
│       └── bucket_man.md       ← バケツマン（デフォルト評価担当）
│
├── templates/                  ← 雛形（編集しない・コピー元）
│   ├── quill_state_template.md
│   └── scene_template.md
│
├── samples/                    ← サンプルプロジェクト（参照用）
│   └── osananajimi_bucket/     ← バケツマン・幼馴染み（チュートリアル用）
│
└── Story/                      ← 作品置き場（作品ごとにサブディレクトリ）
    └── {TITLE}/                ← 作品タイトルのディレクトリ
        ├── state/
        │   └── current.md      ← QUILL_STATE（自動更新・手動編集しない）
        ├── scenes/             ← 書いたシーン本文
        │   └── scene_N.md
        ├── plots/              ← プロット出力（手書き用）
        │   └── plot_vN.md
        └── characters/
            └── main_cast/      ← この作品のキャラクター
```

---

## 読むべきファイル（優先順位）

| 優先度 | ファイル | タイミング |
|-------|---------|---------|
| 1 | `CLAUDE.md`（このファイル） | 常に |
| 2 | `engines/quill_engine.md` | 全フェーズで |
| 3 | `Story/{TITLE}/state/current.md` | セッション開始時・シーン執筆前 |
| 4 | 関連する `Story/{TITLE}/characters/main_cast/` | 今回登場するキャラのみ |
| 5 | `engines/otasuke.md` | おたすけモード有効時 |
| 6 | `engines/eval_engine.md` | シーン完了後の評価時 |
| 7 | `engines/kinsoku.md` | 執筆時・FORMAT設定時 |

---

## 禁止事項

- ユーザーの指示なしにシーンを書き始めない
- おたすけの提案をユーザーが確認する前に執筆を始めない
- `engines/` のファイルを編集しない
- `templates/` のファイルを編集しない（コピー元として保護）
- `Story/{TITLE}/state/current.md` の手動編集をユーザーに提案しない（自動更新のみ）
- 評価（EVAL）をシーン執筆の前に出力しない
