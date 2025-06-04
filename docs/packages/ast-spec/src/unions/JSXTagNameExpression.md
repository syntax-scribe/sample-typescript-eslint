[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `JSXTagNameExpression.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/JSXTagNameExpression.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSXIdentifier` | `../jsx/JSXIdentifier/spec` |
| `JSXMemberExpression` | `../jsx/JSXMemberExpression/spec` |
| `JSXNamespacedName` | `../jsx/JSXNamespacedName/spec` |


---

## Type Aliases

### `JSXTagNameExpression`

```ts
type JSXTagNameExpression = | JSXIdentifier
  | JSXMemberExpression
  | JSXNamespacedName;
```


---