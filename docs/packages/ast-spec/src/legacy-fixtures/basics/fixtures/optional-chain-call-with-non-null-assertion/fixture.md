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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/optional-chain-call-with-non-null-assertion/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `processOptional(one: any): void`

<details><summary>Code</summary>

```ts
function processOptional(one?: any) {
  one?.two!();
  one?.two!.three();
  one?.two!();
  one?.two!.three();
  one?.two!();
  one?.two!.three();
}
```
</details>

- **Parameters**:
  - `one: any`
- **Return Type**: `void`
- **Calls**:
  - `complex_call_113`
  - `one?.two!.three`
  - `complex_call_149`
  - `complex_call_185`

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