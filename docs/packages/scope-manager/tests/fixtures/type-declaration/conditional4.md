[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `conditional4.ts`

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
📂 **`packages/scope-manager/tests/fixtures/type-declaration/conditional4.ts`**

## 🔧 Functions

> No functions found in this file.


---

## Type Aliases

### `Test<U>`

```ts
type Test<U> = U extends { [k: string]: infer I } ? I : never;
```


---