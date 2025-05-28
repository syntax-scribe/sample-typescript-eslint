[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getErrorLabel.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
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
📂 **`packages/ast-spec/tests/util/getErrorLabel.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ErrorLabel` | `./parsers/parser-types.js` |


---

## Functions

### `getErrorLabel(isBabelError: boolean, isTSESTreeError: boolean): ErrorLabel`

<details><summary>Code</summary>

```ts
(
  isBabelError: boolean,
  isTSESTreeError: boolean,
): ErrorLabel => {
  if (!isBabelError && isTSESTreeError) {
    return ErrorLabel.TSESTree;
  }

  if (isBabelError && !isTSESTreeError) {
    return ErrorLabel.Babel;
  }

  if (isBabelError && isTSESTreeError) {
    return ErrorLabel.Both;
  }

  return ErrorLabel.None;
}
```
</details>

- **Parameters**:
  - `isBabelError: boolean`
  - `isTSESTreeError: boolean`
- **Return Type**: `ErrorLabel`

---