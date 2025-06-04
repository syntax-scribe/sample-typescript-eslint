[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSUnaryExpression.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/TSUnaryExpression.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AwaitExpression` | `../expression/AwaitExpression/spec` |
| `UnaryExpression` | `../expression/UnaryExpression/spec` |
| `UpdateExpression` | `../expression/UpdateExpression/spec` |
| `LeftHandSideExpression` | `./LeftHandSideExpression` |


---

## Type Aliases

### `TSUnaryExpression`

```ts
type TSUnaryExpression = | AwaitExpression
  | LeftHandSideExpression
  | UnaryExpression
  | UpdateExpression;
```


---