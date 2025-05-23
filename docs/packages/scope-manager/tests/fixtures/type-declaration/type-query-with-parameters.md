[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `type-query-with-parameters.ts`

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
📂 **`packages/scope-manager/tests/fixtures/type-declaration/type-query-with-parameters.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `foo(y: T): { y: T; }`

<details><summary>Code</summary>

```ts
function foo<T>(y: T) {
  return { y };
}
```
</details>

- **Parameters**:
  - `y: T`
- **Return Type**: `{ y: T; }`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `Foo<T>`

```ts
type Foo<T> = typeof foo<T>;
```


---