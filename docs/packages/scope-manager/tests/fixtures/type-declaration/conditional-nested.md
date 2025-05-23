[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `conditional-nested.ts`

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/conditional-nested.ts`**

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

### `Test<T>`

```ts
type Test<T> = T extends Array<infer U> ? U : T extends Set<infer U> ? U : never;
```


---