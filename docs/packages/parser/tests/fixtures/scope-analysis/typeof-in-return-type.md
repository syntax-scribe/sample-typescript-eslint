[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `typeof-in-return-type.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/typeof-in-return-type.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `f(a: number): typeof a`

<details><summary>Code</summary>

```ts
function f(a: number): typeof a {
  // this `a` is the parameter `a`.
  return 1;
}
```
</details>

- **Parameters**:
  - `a: number`
- **Return Type**: `typeof a`
- **Internal Comments**:
```
// this `a` is the parameter `a`.
```


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