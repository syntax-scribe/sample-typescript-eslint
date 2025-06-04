[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ImportClause.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📑 Type Aliases | 1 |

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

## Type Aliases

### `ImportClause`

```ts
type ImportClause = | ImportDefaultSpecifier
  | ImportNamespaceSpecifier
  | ImportSpecifier;
```


---