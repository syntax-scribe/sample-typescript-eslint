[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `type-arguments2.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/instantiation-expressions/type-arguments2.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `makeBox(value: T): { value: T; }`

<details><summary>Code</summary>

```ts
function makeBox<T>(value: T) {
  return { value };
}
```
</details>

- **Parameters**:
  - `value: T`
- **Return Type**: `{ value: T; }`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `BoxFunc<T>`

```ts
type BoxFunc<T> = typeof makeBox<T>;
```


---