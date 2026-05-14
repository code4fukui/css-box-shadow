# css-box-shadow

軽量で依存関係のない、CSS `box-shadow` のパーサーおよび文字列化ツールです。文字列値と構造化オブジェクト間の変換を行います。

## 機能

- `box-shadow` 文字列を構造化されたオブジェクトの配列にパースします。
- シャドウオブジェクトの配列を有効なCSS文字列に文字列化します。
- カンマ区切りの複数のシャドウをサポートします。
- オプションの `inset` キーワードを正しく処理します。
- さまざまなカラーフォーマット（例: 名前付きカラー、`hex`、`rgba`、`hsla`）をパースします。
- `px` 以外の長さの単位（`em`、`%` など）は、パース時に文字列として保持されます。
- 数値の長さの値は、文字列化の際に `px` に変換されます。
- 省略された `blur-radius` や `spread-radius` の値をインテリジェントに処理します。

## 使い方

ESモジュールから `parse` と `stringify` 関数をインポートします。

```js
import { parse, stringify } from 'https://code4fukui.github.io/css-box-shadow/CSSBoxShadow.js'

// CSS文字列をシャドウオブジェクトの配列にパースします。
const parsed = parse('inset 0 0 0 32px tomato, 0 0 1em rgba(0,0,0,.25)')
/*
[
  {
    inset: true,
    offsetX: 0,
    offsetY: 0,
    blurRadius: 0,
    spreadRadius: 32,
    color: 'tomato'
  },
  {
    inset: false,
    offsetX: 0,
    offsetY: 0,
    blurRadius: '1em',
    spreadRadius: undefined,
    color: 'rgba(0,0,0,.25)'
  }
]
*/

// シャドウオブジェクトの配列をCSS文字列に文字列化します。
const value = stringify([
  {
    offsetX: 4,
    offsetY: 8,
    blurRadius: 0,
    color: 'tomato'
  },
  {
    inset: true,
    spreadRadius: '2px',
    color: '#f00'
  }
])
// '4px 8px 0 tomato, inset 0 0 0 2px #f00'
```

## API

### `parse(string)`

`box-shadow` のCSS文字列を受け取り、シャドウオブジェクトの配列を返します。

- `px` 単位の値は `number` 型に変換されます（例: `'10px'` は `10` になります）。
- その他の単位（`em`、`rem`、`%` など）を持つ値は、`string` 型として保持されます。

### `stringify(Array<Object>)`

シャドウオブジェクトの配列を受け取り、`box-shadow` のCSS文字列を返します。

- 長さの `number` 値は `px` 文字列に変換されます（例: `10` は `'10px'` になります）。ただし、`0` は `0` のままです。
- 長さの `string` 値はそのまま使用されます。
- `offsetX`、`offsetY`、`blurRadius` が欠落している場合は、デフォルトで `0` になります。
- `spreadRadius` と `color` が欠落している場合は、出力から省略されます。

### シャドウオブジェクト

`parse` および `stringify` 関数は、以下の構造を持つオブジェクトを使用します。

- `inset` (`boolean`): シャドウが inset の場合は `true`。デフォルトは `false` です。
- `offsetX` (`number | string`): 水平方向のオフセット。
- `offsetY` (`number | string`): 垂直方向のオフセット。
- `blurRadius` (`number | string | undefined`): ぼかし半径（blur radius）。
- `spreadRadius` (`number | string | undefined`): 拡散半径（spread radius）。
- `color` (`string | undefined`): CSSのカラー値。

## ライセンス

MIT License — 詳細は [LICENSE](LICENSE) を参照してください。
