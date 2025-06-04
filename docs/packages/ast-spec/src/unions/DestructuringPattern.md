[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `DestructuringPattern.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 6 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/DestructuringPattern.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Identifier` | `../expression/Identifier/spec` |
| `MemberExpression` | `../expression/MemberExpression/spec` |
| `ArrayPattern` | `../parameter/ArrayPattern/spec` |
| `AssignmentPattern` | `../parameter/AssignmentPattern/spec` |
| `ObjectPattern` | `../parameter/ObjectPattern/spec` |
| `RestElement` | `../parameter/RestElement/spec` |


---

## Type Aliases

### `DestructuringPattern`

```ts
type DestructuringPattern = | ArrayPattern
  | AssignmentPattern
  | Identifier
  | MemberExpression
  | ObjectPattern
  | RestElement;
```


---