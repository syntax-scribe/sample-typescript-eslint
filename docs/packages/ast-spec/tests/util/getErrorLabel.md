[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getErrorLabel.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 1 |

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