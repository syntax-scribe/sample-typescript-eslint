[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `NoInfer.ts`

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/utils/src/ts-utils/NoInfer.ts`**

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

### `NoInfer<A>`

/**
 * We could use NoInfer typescript build-in utility
 * introduced in typescript 5.4, however at the moment of creation
 * the supported ts versions are >=4.8.4 <5.7.0
 * so for the moment we have to stick to this polyfill.
 *
 * @see https://github.com/millsp/ts-toolbelt/blob/master/sources/Function/NoInfer.ts
 */

```ts
type NoInfer<A> = [A][A extends unknown ? 0 : never];
```


---