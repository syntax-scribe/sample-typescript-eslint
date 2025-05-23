[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types-nested-types.src.ts`

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/types-nested-types.src.ts`**

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

### `Foo`

```ts
type Foo = | [number, string?, boolean?]
  | ([{}, [number?] | (null & boolean[])] & {});
```


---