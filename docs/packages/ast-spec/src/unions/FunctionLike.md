[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `FunctionLike.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

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