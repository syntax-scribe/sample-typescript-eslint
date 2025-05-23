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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/optional-chain-call-with-parens/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `processOptionalCallParens(one: any): void`

<details><summary>Code</summary>

```ts
function processOptionalCallParens(one?: any) {
  one?.fn();
  (one?.two).fn();
  one.two?.fn();
  (one.two?.three).fn();
  one.two?.three?.fn();

  one?.();
  (one?.())();
  one?.()?.();

  (one?.()).two;
}
```
</details>

- **Parameters**:
  - `one: any`
- **Return Type**: `void`
- **Calls**:
  - `one?.fn`
  - `(one?.two).fn`
  - `one.two?.fn`
  - `(one.two?.three).fn`
  - `one.two?.three?.fn`
  - `one`
  - `complex_call_233`
  - `complex_call_248`

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