[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `assert.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/assert.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `assert(value: unknown, message: string): asserts value`

<details><summary>Code</summary>

```ts
export function assert(value: unknown, message?: string): asserts value {
  if (value == null) {
    throw new Error(message);
  }
}
```
</details>

- **Parameters**:
  - `value: unknown`
  - `message: string`
- **Return Type**: `asserts value`

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