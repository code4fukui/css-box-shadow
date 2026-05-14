# css-box-shadow

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

A lightweight, zero-dependency CSS `box-shadow` parser and stringifier for converting between string values and structured objects.

## Features

-   Parse `box-shadow` strings into an array of structured objects.
-   Stringify an array of shadow objects back into a valid CSS string.
-   Supports multiple, comma-separated shadows.
-   Correctly handles the optional `inset` keyword.
-   Parses various color formats (e.g., named, `hex`, `rgba`, `hsla`).
-   Preserves non-`px` length units (like `em`, `%`) as strings during parsing.
-   Converts numeric length values to `px` during stringification.
-   Intelligently handles omitted `blur-radius` and `spread-radius` values.

## Usage

Import the `parse` and `stringify` functions from the ES module.

```js
import { parse, stringify } from 'https://code4fukui.github.io/css-box-shadow/CSSBoxShadow.js'

// Parse a CSS string into an array of shadow objects.
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

// Stringify an array of shadow objects back to a CSS string.
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

Takes a `box-shadow` CSS string and returns an array of shadow objects.

-   Values with `px` units are converted to `number` types (e.g., `'10px'` becomes `10`).
-   Values with other units (`em`, `rem`, `%`, etc.) are preserved as `string` types.

### `stringify(Array<Object>)`

Takes an array of shadow objects and returns a `box-shadow` CSS string.

-   `number` values for lengths are converted to `px` strings (e.g., `10` becomes `'10px'`), except for `0`, which remains `0`.
-   `string` values for lengths are used as-is.
-   Missing `offsetX`, `offsetY`, and `blurRadius` default to `0`.
-   Missing `spreadRadius` and `color` are omitted from the output.

### The Shadow Object

The `parse` and `stringify` functions use objects with the following structure:

-   `inset` (`boolean`): `true` if the shadow is inset. Defaults to `false`.
-   `offsetX` (`number | string`): The horizontal offset.
-   `offsetY` (`number | string`): The vertical offset.
-   `blurRadius` (`number | string | undefined`): The blur radius.
-   `spreadRadius` (`number | string | undefined`): The spread radius.
-   `color` (`string | undefined`): The CSS color value.

## License

MIT License — see [LICENSE](LICENSE).