[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `mapped-named.ts`

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/mapped-named.ts`**

## 📦 Imports

> No imports found in this file.


---

## 🔧 Functions

> No functions found in this file.


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
type T = Record<string, string>;
```

### `A`

```ts
type A = { [k in string as k]: T[k] };
```


---