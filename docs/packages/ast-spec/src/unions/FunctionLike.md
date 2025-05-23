[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `FunctionLike.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/FunctionLike.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `FunctionDeclaration` | `../declaration/FunctionDeclaration/spec` |
| `TSDeclareFunction` | `../declaration/TSDeclareFunction/spec` |
| `ArrowFunctionExpression` | `../expression/ArrowFunctionExpression/spec` |
| `FunctionExpression` | `../expression/FunctionExpression/spec` |
| `TSEmptyBodyFunctionExpression` | `../expression/TSEmptyBodyFunctionExpression/spec` |


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

### `FunctionLike`

```ts
type FunctionLike = | ArrowFunctionExpression
  | FunctionDeclaration
  | FunctionExpression
  | TSDeclareFunction
  | TSEmptyBodyFunctionExpression;
```


---