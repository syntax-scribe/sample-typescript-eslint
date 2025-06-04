[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `serialize-error.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/util/serialize-error.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `codeFrameColumns` | `@babel/code-frame` |
| `TSError` | `./parsers/typescript-estree-import` |


---

## Functions

### `serializeError(error: unknown, contents: string): unknown`

<details><summary>Code</summary>

```ts
export function serializeError(error: unknown, contents: string): unknown {
  if (!(error instanceof TSError)) {
    return error;
  }

  const {
    location: { end, start },
    message,
    name,
  } = error;

  return `${name}
${codeFrameColumns(
  contents,
  {
    end: { column: end.column + 1, line: end.line },
    start: { column: start.column + 1, line: start.line },
  },
  { highlightCode: false, message },
)}`;
}
```
</details>

- **Parameters**:
  - `error: unknown`
  - `contents: string`
- **Return Type**: `unknown`
- **Calls**:
  - `codeFrameColumns (from @babel/code-frame)`

---