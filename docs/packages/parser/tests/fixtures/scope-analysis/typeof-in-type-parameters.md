[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `typeof-in-type-parameters.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/typeof-in-type-parameters.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `g(g: T): number`

<details><summary>Code</summary>

```ts
function g<T extends typeof g>(g: T): number {
  return 1;
}
```
</details>

- **Parameters**:
  - `g: T`
- **Return Type**: `number`

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