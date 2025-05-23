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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/readonly-arrays/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `foo(arr: ReadonlyArray<string>): void`

<details><summary>Code</summary>

```ts
function foo(arr: ReadonlyArray<string>) {
  arr.slice(); // okay
  arr.push('hello!'); // error!
}
```
</details>

- **Parameters**:
  - `arr: ReadonlyArray<string>`
- **Return Type**: `void`
- **Calls**:
  - `arr.slice`
  - `arr.push`

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