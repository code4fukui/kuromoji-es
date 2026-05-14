# kuromoji-es

[
![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)
](https://opensource.org/licenses/Apache-2.0)

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

A Japanese morphological analyzer implemented as a pure JavaScript ES module. This is a modern port of the original [Kuromoji](https://www.atilika.com/ja/kuromoji/), designed for simplicity and compatibility with current web standards.

## Features

-   **Pure JavaScript:** Runs in any modern JavaScript environment without native dependencies.
-   **ES Module:** Easily importable into modern projects using `import`.
-   **Cross-Platform:** Works seamlessly in Deno and modern web browsers.
-   **Optimized:** Uses compressed dictionary files (gzip) for faster network loading.

## Usage

Import `kuromoji-es` and use the async `createTokenizer` function to get a tokenizer instance. The dictionary is loaded from a remote CDN by default.

```js
import { kuromoji } from "https://code4fukui.github.io/kuromoji-es/kuromoji.js";

// Asynchronously load the dictionary and create a tokenizer
const tokenizer = await kuromoji.createTokenizer();

// Tokenize a sentence
const tokens = tokenizer.tokenize("すもももももももものうち");

console.log(tokens);
```

## API Reference

### `kuromoji.createTokenizer()`

Asynchronously loads the dictionary files and returns a `Promise` that resolves with a tokenizer instance.

### `tokenizer.tokenize(text)`

Takes a string of Japanese text and returns an array of token objects, each containing detailed morphological information.

### Token Object Structure

The `tokenize()` method returns an array of objects with the following structure:

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

**Fields:**

-   `word_id`: ID of the word in the dictionary.
-   `word_type`: Type of word (`KNOWN` if in dictionary, `UNKNOWN` otherwise).
-   `word_position`: 1-based starting position of the word in the input text.
-   `surface_form`: The word as it appears in the text.
-   `pos`: Part of speech (e.g., `名詞` for noun).
-   `pos_detail_1`, `pos_detail_2`, `pos_detail_3`: Sub-classifications for the part of speech.
-   `conjugated_type`: Conjugation type (e.g., `五段・ラ行` for Godan verb).
-   `conjugated_form`: Conjugation form (e.g., `基本形` for basic form).
-   `basic_form`: The base form (lemma) of the word.
-   `reading`: The reading of the word in Katakana.
-   `pronunciation`: The pronunciation of the word in Katakana.

For more details on the dictionary fields, please refer to the original [kuromoji.js JSDoc page](https://takuyaa.github.io/kuromoji.js/jsdoc/).

## Acknowledgements

This project is a port of [kuromoji.js](https://github.com/takuyaa/kuromoji.js/) by Takuya Asano, which is a JavaScript port of the original [Kuromoji](https://www.atilika.com/ja/kuromoji/) project by Atilika Inc.

## License

This library is licensed under the Apache License, Version 2.0.