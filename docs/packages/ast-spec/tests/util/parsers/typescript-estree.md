[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `typescript-estree.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

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