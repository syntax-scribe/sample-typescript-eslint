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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/readonly-tuples/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `foo(pair: readonly [string, string]): void`

<details><summary>Code</summary>

```ts
function foo(pair: readonly [string, string]) {
  console.log(pair[0]); // okay
  pair[1] = 'hello!'; // error
}
```
</details>

- **Parameters**:
  - `pair: readonly [string, string]`
- **Return Type**: `void`
- **Calls**:
  - `console.log`

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