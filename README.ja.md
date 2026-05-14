# kuromoji-es

[
![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)
](https://opensource.org/licenses/Apache-2.0)

ピュアJavaScriptのESモジュールとして実装された日本語形態素解析器です。オリジナルの[Kuromoji](https://www.atilika.com/ja/kuromoji/)を現代的な仕様に移植し、シンプルさと最新のウェブ標準との互換性を重視して設計されています。

## 機能

-   **ピュアJavaScript:** ネイティブ依存関係なしに、最新のJavaScript環境で動作します。
-   **ESモジュール:** `import`を使用して、モダンなプロジェクトへ簡単に組み込むことができます。
-   **クロスプラットフォーム:** Denoや最新のウェブブラウザでシームレスに動作します。
-   **最適化:** 圧縮された辞書ファイル（gzip）を使用し、ネットワークの読み込みを高速化しています。

## 使い方

`kuromoji-es`をインポートし、非同期関数の`createTokenizer`を使用してトークナイザーのインスタンスを取得します。辞書はデフォルトでリモートCDNから読み込まれます。

```js
import { kuromoji } from "https://code4fukui.github.io/kuromoji-es/kuromoji.js";

// 辞書を非同期で読み込み、トークナイザーを生成
const tokenizer = await kuromoji.createTokenizer();

// 文のトークン化
const tokens = tokenizer.tokenize("すもももももももものうち");

console.log(tokens);
```

## APIリファレンス

### `kuromoji.createTokenizer()`

辞書ファイルを非同期で読み込み、トークナイザーのインスタンスで解決される`Promise`を返します。

### `tokenizer.tokenize(text)`

日本語テキストの文字列を受け取り、詳細な形態素情報を含むトークンオブジェクトの配列を返します。

### トークンオブジェクトの構造

`tokenize()`メソッドは、以下の構造を持つオブジェクトの配列を返します。

```json
[
  {
    "word_id": 509800,
    "word_type": "KNOWN",
    "word_position": 1,
    "surface_form": "黒文字",
    "pos": "名詞",
    "pos_detail_1": "一般",
    "pos_detail_2": "*",
    "pos_detail_3": "*",
    "conjugated_type": "*",
    "conjugated_form": "*",
    "basic_form": "黒文字",
    "reading": "クロモジ",
    "pronunciation": "クロモジ"
  }
]
```

**フィールド:**

-   `word_id`: 辞書内での単語ID。
-   `word_type`: 単語のタイプ（辞書に存在する場合は`KNOWN`、未登録語の場合は`UNKNOWN`）。
-   `word_position`: 1から始まる入力テキスト内での単語の開始位置。
-   `surface_form`: テキスト内に出現する単語の表層形。
-   `pos`: 品詞（例: `名詞`）。
-   `pos_detail_1`, `pos_detail_2`, `pos_detail_3`: 品詞細分類。
-   `conjugated_type`: 活用型（例: `五段・ラ行`）。
-   `conjugated_form`: 活用形（例: `基本形`）。
-   `basic_form`: 単語の基本形。
-   `reading`: 単語の読み（カタカナ）。
-   `pronunciation`: 単語の発音（カタカナ）。

辞書の各フィールドの詳細については、オリジナルの[kuromoji.js JSDocページ](https://takuyaa.github.io/kuromoji.js/jsdoc/)をご参照ください。

## 謝辞

本プロジェクトは、Takuya Asano氏による[kuromoji.js](https://github.com/takuyaa/kuromoji.js/)の移植版です。同ライブラリは、Atilika Inc.によるオリジナルの[Kuromoji](https://www.atilika.com/ja/kuromoji/)プロジェクトをJavaScriptに移植したものです。

## ライセンス

本ライブラリはApache License, Version 2.0の下でライセンスされています。
