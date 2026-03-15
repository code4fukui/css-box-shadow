# CSS Box Shadowパーサーとストリンガー

CSSのbox-shadowプロパティをパースし、文字列に変換するライブラリです。

## デモ
サンプルコードは以下の通りです。

```js
import { parse, stringify } from 'https://code4fukui.github.io/css-box-shadow/CSSBoxShadow.js'

// CSSの文字列をパースしてオブジェクトの配列に変換
const parsed = parse('0 0 0 32px tomato')
// [{ inset: false,
//   offsetX: 0,
//   offsetY: 0,
//   blurRadius: 0,
//   spreadRadius: 32,
//   color: 'tomato' }]

// オブジェクトの配列からbox-shadowの文字列を生成
const value = stringify(parsed)
// '0 0 0 32px tomato'
```

## 機能
- CSSのbox-shadowプロパティをパースしてオブジェクトの配列に変換
- オブジェクトの配列からbox-shadowの文字列を生成

## 使い方
このライブラリをWebページに読み込むことで、`parse`および`stringify`関数が利用できます。

```html
<script type="module">
import { parse, stringify } from 'https://code4fukui.github.io/css-box-shadow/CSSBoxShadow.js'
</script>
```

## ライセンス
MIT License