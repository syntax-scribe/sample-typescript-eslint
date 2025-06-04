[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ChainElement.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/ChainElement.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `CallExpression` | `../expression/CallExpression/spec` |
| `MemberExpression` | `../expression/MemberExpression/spec` |
| `TSNonNullExpression` | `../expression/TSNonNullExpression/spec` |


---

## Type Aliases

### `ChainElement`

```ts
type ChainElement = | CallExpression
  | MemberExpression
  | TSNonNullExpression;
```


---