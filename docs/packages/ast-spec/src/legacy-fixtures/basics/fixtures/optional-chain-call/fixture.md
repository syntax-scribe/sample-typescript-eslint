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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/optional-chain-call/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `processOptionalCall(one: any): void`

<details><summary>Code</summary>

```ts
function processOptionalCall(one?: any) {
  one?.fn();
  one?.two.fn();
  one.two?.fn();
  one.two?.three.fn();
  one.two?.three?.fn();

  one?.();
  one?.()();
  one?.()?.();

  one?.().two;
}
```
</details>

- **Parameters**:
  - `one: any`
- **Return Type**: `void`
- **Calls**:
  - `one?.fn`
  - `one?.two.fn`
  - `one.two?.fn`
  - `one.two?.three.fn`
  - `one.two?.three?.fn`
  - `one`
  - `complex_call_223`
  - `complex_call_236`

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