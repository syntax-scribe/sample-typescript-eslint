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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/optional-chain-element-access/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `processOptionalElement(one: any): void`

<details><summary>Code</summary>

```ts
function processOptionalElement(one?: any) {
  one?.[2];
  one?.[2][3];
  one[2]?.[3];
  one[2]?.[3];
  one[2]?.[3][4];
  one[2]?.[3]?.[4];
}
```
</details>

- **Parameters**:
  - `one: any`
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