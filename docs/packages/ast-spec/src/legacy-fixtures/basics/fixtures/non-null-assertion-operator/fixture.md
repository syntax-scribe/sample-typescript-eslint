[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/non-null-assertion-operator/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `processEntity(e: Entity): void`

<details><summary>Code</summary>

```ts
function processEntity(e?: Entity) {
  validateEntity(e);
  let s = e!.name;
}
```
</details>

- **Parameters**:
  - `e: Entity`
- **Return Type**: `void`
- **Calls**:
  - `validateEntity`

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