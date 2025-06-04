[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TypeElement.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📑 Type Aliases | 1 |

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