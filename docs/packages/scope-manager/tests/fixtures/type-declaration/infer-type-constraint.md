[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `infer-type-constraint.ts`

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/infer-type-constraint.ts`**

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

### `X`

```ts
type X = string | number;
```

### `Id<T>`

```ts
type Id<T> = T extends { id: infer Id extends X } ? Id : never;
```


---