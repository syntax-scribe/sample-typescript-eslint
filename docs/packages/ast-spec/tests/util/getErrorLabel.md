[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getErrorLabel.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---