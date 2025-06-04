[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `JSXChild.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/JSXChild.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSXElement` | `../expression/JSXElement/spec` |
| `JSXFragment` | `../expression/JSXFragment/spec` |
| `JSXText` | `../jsx/JSXText/spec` |
| `JSXExpression` | `./JSXExpression` |


---

## Type Aliases

### `JSXChild`

```ts
type JSXChild = JSXElement | JSXExpression | JSXFragment | JSXText;
```


---