[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types-intersection-type.src.ts`

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
📂 **`packages/parser/tests/fixtures/scope-analysis/types-intersection-type.src.ts`**

## 🔧 Functions

> No functions found in this file.


---

## Type Aliases

### `LinkedList<T>`

```ts
type LinkedList<T> = T & { next: LinkedList<T> };
```


---