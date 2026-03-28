# QUILL_STATE テンプレート

このファイルは雛形です。編集しないでください。
`state/current.md` を新規作成する際にコピーして使います。

---

```
<<QUILL_STATE>>
STATUS:new
TITLE:
GENRE:
PREMISE:
TARGET_VOL:
FORMAT:default
OUTLINE_MODE:

CHAR:{コード}|{名前}|{年齢・立場}|{性格・特徴}|wants:{欲望}→but:{矛盾}|{口調}

REL:{Aコード}>{Bコード}|好意{0-9},緊張{0-9},距離{0-9}|{関係メモ}

OUTLINE:{番号}|{機能:起/承/転/結/自由}|{場所}|{目的}|{必須要素}

EVAL_CHAR:BM
PROGRESS:0
MEMO:
<</QUILL_STATE>>
```

---

## フィールド記入例

```
<<QUILL_STATE>>
STATUS:writing
TITLE:幼馴染みとバケツ頭
GENRE:ラブコメ・ライトノベル
PREMISE:幼馴染みの恋心に無自覚な女子高生が、バケツ頭YouTuberの助言を頼りに告白を迫る
TARGET_VOL:短編
FORMAT:default
OUTLINE_MODE:basic

CHAR:FG|幼馴染み（女）|高校生|恋愛に無自覚な楽観主義者|wants:幼馴染みに告白されたい→but:自分が先に好きだと気づいていない|素直で突っ走りやすい
CHAR:BM|バケツマン|高校生YouTuber|バケツ型ヘルメットの高校生セラピスト|wants:リスナーの悩みを解決したい→but:アドバイスが的外れで妙に当たる|断言口調、短文
CHAR:FM|幼馴染み（男）|高校生|好意を隠して待っている|wants:幼馴染みに気づいてほしい→but:伝える気がなく「待つ」を選んでいる|ツッコミ気質、短め

REL:FG>FM|好意7,緊張3,距離2|幼馴染み。好意に無自覚
REL:FG>BM|好意5,緊張0,距離8|配信者とリスナー。FGはBMが幼馴染みだと知らない
REL:FM>BM|好意9,緊張0,距離0|同一人物

OUTLINE:1|起|学校・日常|幼馴染みの日常とバケツマンへの依存を導入|バケツマンの名言を自然に出す
OUTLINE:2|承|映画・デート後|デートっぽい誘いと「普通すぎる反応」の居心地悪さ|FGの自己矛盾を見せる
OUTLINE:3|転|配信・自室|5000円スパチャのやり取りが転換点になる|バケツマンの言葉で決意する
OUTLINE:4|結|校舎裏|告白シーン → 「伝わってるから待ってた」|FGの自覚、FMの本音開示

EVAL_CHAR:BM
PROGRESS:0
MEMO:
<</QUILL_STATE>>
```
