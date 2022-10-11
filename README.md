# css-box-shadow

CSS box shadow parser and stringifier

```js
import { parse, stringify } from 'https://code4fukui.github.io/css-box-shadow/CSSBoxShadow.js'

// parse a CSS string value into an array of objects
const parsed = parse('0 0 0 32px tomato')
// [{ inset: false,
//   offsetX: 0,
//   offsetY: 0,
//   blurRadius: 0,
//   spreadRadius: 32,
//   color: 'tomato' }]

// convert an array of objects into a box-shadow string value
const value = stringify(parsed)
// '0 0 0 32px tomato'
```

MIT License
