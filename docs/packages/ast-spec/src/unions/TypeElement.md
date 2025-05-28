[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TypeElement.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
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
📂 **`packages/ast-spec/src/unions/TypeElement.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSCallSignatureDeclaration` | `../element/TSCallSignatureDeclaration/spec` |
| `TSConstructSignatureDeclaration` | `../element/TSConstructSignatureDeclaration/spec` |
| `TSIndexSignature` | `../element/TSIndexSignature/spec` |
| `TSMethodSignature` | `../element/TSMethodSignature/spec` |
| `TSPropertySignature` | `../element/TSPropertySignature/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Type Aliases

### `TypeElement`

```ts
type TypeElement = | TSCallSignatureDeclaration
  | TSConstructSignatureDeclaration
  | TSIndexSignature
  | TSMethodSignature
  | TSPropertySignature;
```


---