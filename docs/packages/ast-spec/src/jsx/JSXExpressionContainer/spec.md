[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/jsx/JSXExpressionContainer/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |
| `JSXEmptyExpression` | `../JSXEmptyExpression/spec` |


---

## Interfaces

### `JSXExpressionContainer`

<details><summary>Interface Code</summary>

```ts
export interface JSXExpressionContainer extends BaseNode {
  type: AST_NODE_TYPES.JSXExpressionContainer;
  expression: Expression | JSXEmptyExpression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.JSXExpressionContainer` | ✗ |  |
| `expression` | `Expression | JSXEmptyExpression` | ✗ |  |


---