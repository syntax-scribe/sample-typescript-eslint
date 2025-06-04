[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `JSXTagNameExpression.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
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
📂 **`packages/ast-spec/src/unions/JSXTagNameExpression.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSXIdentifier` | `../jsx/JSXIdentifier/spec` |
| `JSXMemberExpression` | `../jsx/JSXMemberExpression/spec` |
| `JSXNamespacedName` | `../jsx/JSXNamespacedName/spec` |


---


---

## Type Aliases

### `JSXTagNameExpression`

```ts
type JSXTagNameExpression = | JSXIdentifier
  | JSXMemberExpression
  | JSXNamespacedName;
```


---