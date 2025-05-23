[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `readable-ref-nested-body-shadow.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/functions/function-expression/default-params/readable-ref-nested-body-shadow.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `foo(b: () => void): void`

<details><summary>Code</summary>

```ts
function (
  b = function () {
    a;
  },
) {
  let a;
}
```
</details>

- **Parameters**:
  - `b: () => void`
- **Return Type**: `void`

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