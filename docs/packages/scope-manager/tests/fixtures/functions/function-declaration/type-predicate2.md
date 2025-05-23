[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `type-predicate2.ts`

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
📂 **`packages/scope-manager/tests/fixtures/functions/function-declaration/type-predicate2.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `foo(arg: any): arg is T`

<details><summary>Code</summary>

```ts
function foo(arg: any): arg is T {
  return typeof arg === 'string';
}
```
</details>

- **Parameters**:
  - `arg: any`
- **Return Type**: `arg is T`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `T`

```ts
type T = string;
```


---