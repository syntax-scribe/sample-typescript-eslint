[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Parameter.ts`

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