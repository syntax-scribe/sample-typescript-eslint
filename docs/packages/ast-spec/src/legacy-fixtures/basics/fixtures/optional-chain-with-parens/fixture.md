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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/optional-chain-with-parens/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `processOptionalParens(one: any): void`

<details><summary>Code</summary>

```ts
function processOptionalParens(one?: any) {
  one?.two;
  (one?.two).three;
  one.two?.three;
  (one.two?.three).four;
  one.two?.three?.four;
  (one.two?.three?.four).five;
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