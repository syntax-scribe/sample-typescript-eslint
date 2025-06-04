[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `JSXChild.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
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

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/JSXChild.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSXElement` | `../expression/JSXElement/spec` |
| `JSXFragment` | `../expression/JSXFragment/spec` |
| `JSXText` | `../jsx/JSXText/spec` |
| `JSXExpression` | `./JSXExpression` |


---


---

## Type Aliases

### `JSXChild`

```ts
type JSXChild = JSXElement | JSXExpression | JSXFragment | JSXText;
```


---