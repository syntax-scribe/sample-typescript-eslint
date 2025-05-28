[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `infer-type-constraint.ts`

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
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/infer-type-constraint.ts`**

## 🔧 Functions

> No functions found in this file.


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