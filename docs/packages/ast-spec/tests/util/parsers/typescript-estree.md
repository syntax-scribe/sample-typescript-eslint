[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `typescript-estree.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/util/parsers/typescript-estree.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Fixture` | `./parser-types.js` |
| `ParserResponse` | `./parser-types.js` |
| `ParserResponseType` | `./parser-types.js` |
| `parse` | `./typescript-estree-import.js` |


---

## Functions

### `parseTSESTree(fixture: Pick<Fixture, 'config' | 'contents' | 'isJSX'>): ParserResponse`

<details><summary>Code</summary>

```ts
export function parseTSESTree(
  fixture: Pick<Fixture, 'config' | 'contents' | 'isJSX'>,
): ParserResponse {
  try {
    const result = parse(fixture.contents, {
      allowInvalidAST: fixture.config.allowInvalidAST,
      comment: false,
      jsx: fixture.isJSX,
      loc: true,
      range: true,
      suppressDeprecatedPropertyWarnings: true,
      tokens: true,
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
  - `fixture: Pick<Fixture, 'config' | 'contents' | 'isJSX'>`
- **Return Type**: `ParserResponse`
- **Calls**:
  - `parse (from ./typescript-estree-import.js)`

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