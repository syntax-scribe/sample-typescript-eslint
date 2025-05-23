[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isReadonlyArray.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/isReadonlyArray.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `isReadonlyArray(arg: unknown): arg is readonly unknown[]`

<details><summary>Code</summary>

```ts
export function isReadonlyArray(arg: unknown): arg is readonly unknown[] {
  return Array.isArray(arg);
}
```
</details>

- **Parameters**:
  - `arg: unknown`
- **Return Type**: `arg is readonly unknown[]`
- **Calls**:
  - `Array.isArray`

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