[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `DestructuringPattern.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 1

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

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


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