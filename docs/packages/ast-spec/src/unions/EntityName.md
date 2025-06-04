[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `EntityName.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/EntityName.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Identifier` | `../expression/Identifier/spec` |
| `ThisExpression` | `../expression/ThisExpression/spec` |
| `TSQualifiedName` | `../type/TSQualifiedName/spec` |


---

## Type Aliases

### `EntityName`

```ts
type EntityName = Identifier | ThisExpression | TSQualifiedName;
```


---