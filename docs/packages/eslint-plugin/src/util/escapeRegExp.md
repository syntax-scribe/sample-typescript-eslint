[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `escapeRegExp.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/escapeRegExp.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `escapeRegExp(string: string): string`

<details><summary>Code</summary>

```ts
export function escapeRegExp(string = ''): string {
  return string && reHasRegExpChar.test(string)
    ? string.replaceAll(reRegExpChar, '\\$&')
    : string;
}
```
</details>

- **Parameters**:
  - `string: string`
- **Return Type**: `string`
- **Calls**:
  - `reHasRegExpChar.test`
  - `string.replaceAll`

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