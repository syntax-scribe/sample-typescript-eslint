[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Parameter.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 6 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/Parameter.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Identifier` | `../expression/Identifier/spec` |
| `ArrayPattern` | `../parameter/ArrayPattern/spec` |
| `AssignmentPattern` | `../parameter/AssignmentPattern/spec` |
| `ObjectPattern` | `../parameter/ObjectPattern/spec` |
| `RestElement` | `../parameter/RestElement/spec` |
| `TSParameterProperty` | `../parameter/TSParameterProperty/spec` |


---

## Type Aliases

### `Parameter`

```ts
type Parameter = | ArrayPattern
  | AssignmentPattern
  | Identifier
  | ObjectPattern
  | RestElement
  | TSParameterProperty;
```


---