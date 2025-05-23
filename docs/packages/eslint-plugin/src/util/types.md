[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `types.ts`

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/types.ts`**

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

### `MakeRequired<Base, Key extends keyof Base extends keyof Base>`

```ts
type MakeRequired<Base, Key extends keyof Base extends keyof Base> = Omit<Base, Key> &
  Required<Record<Key, NonNullable<Base[Key]>>>;
```

### `ValueOf<T>`

```ts
type ValueOf<T> = T[keyof T];
```


---