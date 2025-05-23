[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `babel.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/util/parsers/babel.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserOptions` | `@babel/core` |
| `parse` | `@babel/eslint-parser` |
| `Fixture` | `./parser-types.js` |
| `ParserResponse` | `./parser-types.js` |
| `ParserResponseType` | `./parser-types.js` |


---

## Functions

### `parseBabel(fixture: Pick<Fixture, 'contents' | 'isJSX'>): ParserResponse`

<details><summary>Code</summary>

```ts
export function parseBabel(
  fixture: Pick<Fixture, 'contents' | 'isJSX'>,
): ParserResponse {
  const plugins = [...PLUGINS];
  if (fixture.isJSX) {
    plugins.push('jsx');
  }

  try {
    const result = parse(fixture.contents, {
      allowImportExportEverywhere: true,
      babelOptions: {
        parserOpts: {
          plugins,
        },
      },
      ecmaFeatures: {
        globalReturn: true,
      },
      requireConfigFile: false,
      sourceType: 'unambiguous',
    });
    const { comments: __, tokens, ...ast } = result;

    return {
      ast,
      error: 'NO ERROR',
      tokens,
      type: ParserResponseType.NoError,
    };
  } catch (error: unknown) {
    return {
      error,
      type: ParserResponseType.Error,
    };
  }
}
```
</details>

- **Parameters**:
  - `fixture: Pick<Fixture, 'contents' | 'isJSX'>`
- **Return Type**: `ParserResponse`
- **Calls**:
  - `plugins.push`
  - `parse (from @babel/eslint-parser)`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---