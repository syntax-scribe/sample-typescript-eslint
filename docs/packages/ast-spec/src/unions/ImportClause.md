[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ImportClause.ts`

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
📂 **`packages/ast-spec/src/unions/ImportClause.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ImportDefaultSpecifier` | `../special/ImportDefaultSpecifier/spec` |
| `ImportNamespaceSpecifier` | `../special/ImportNamespaceSpecifier/spec` |
| `ImportSpecifier` | `../special/ImportSpecifier/spec` |


---


---

## Type Aliases

### `ImportClause`

```ts
type ImportClause = | ImportDefaultSpecifier
  | ImportNamespaceSpecifier
  | ImportSpecifier;
```


---