# うーちーをさがせ

にせものの中にまぎれた、本物のうーちーを見つけ出すゲーム。

Game Design: YMD

## 遊ぶ

▶ **https://ユーザー名.github.io/uuchii-sagase/**
（GitHub Pages を有効にすると、このURLで遊べる。「ユーザー名」を自分のものに書きかえてね）

スマホのブラウザでそのまま遊べる。記録（図鑑・ランキング・続きから）は、遊んだ端末のブラウザの中に保存される。

## あそびかた

- はじめての人は、メニューの「はじめての人はこちら」から。4つの練習で遊び方を覚えられる
- 右上の小窓に、本物のうーちーの今の姿がいつも映っている。同じ柄の子を探してタップ
- にせものは、耳・つの・おしり・しっぽ・手足・ソフトクリームの味など、どこかがちがう
- エンドレスは持ち時間60秒。本物を見つけると+20秒、にせものをタップすると−5秒
- タイトルの「観察モード」では、集めた子をのんびり眺められる

## 中身

| ファイル・フォルダ | 中身 |
|---|---|
| `index.html` | ゲーム本体 |
| `viewer/uuchii-model.html` | うーちーのモデルの制作ビュー |
| `models/` | N64風のうーちーのモデル（近く用 約500三角形・遠く用 約200三角形）。GLB / OBJ / テクスチャ |
| `source_500/`・`source_200/` | モデルとテクスチャを作るPythonスクリプト |
| `tools/inject.py` | 作り直したモデルを、ゲームと制作ビューに埋め込むスクリプト |

## モデルを作り直す

Python 3 と `numpy`・`Pillow` が必要。

```
pip install numpy pillow
cd source_500 && python3 paint.py && python3 export.py && cd ..
cd source_200 && python3 paint.py && python3 export.py && cd ..
python3 tools/inject.py
```

- `build.py` … 形（頂点・三角形・UV）
- `paint.py` … テクスチャを全部コードで描く（にせもの用の模様は `layer_*.png` として別に書き出す）
- `export.py` … `models/` に GLB・OBJ を、スクリプトと同じ場所に `export.json` を書き出す
- `render.py` … 確認用の簡易レンダラー

## ゲームの主な設定（index.html の中）

- `RULES` … 持ち時間・ペナルティ・出現率などの数字
- `STAGES` / `TUT_STAGES` … エンドレス序盤の5面と、チュートリアルの4面
- `ASSETS.diffs` … にせものの違い（名前・セリフ）
- `ZUKAN_CATS` … 図鑑のカテゴリ
- `CHAT_LINES` など … うーちーのセリフ

起動するたびに設定の自己チェックが走り、欠けがあると画面上部に赤い帯で表示される。
