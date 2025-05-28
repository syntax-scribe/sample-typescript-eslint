[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `NoInfer.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/utils/src/ts-utils/NoInfer.ts`**

## 🔧 Functions

> No functions found in this file.


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