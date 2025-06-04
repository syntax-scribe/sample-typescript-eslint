[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/type/TSLiteralType/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `UnaryExpression` | `../../expression/UnaryExpression/spec` |
| `UpdateExpression` | `../../expression/UpdateExpression/spec` |
| `LiteralExpression` | `../../unions/LiteralExpression` |


---

## Interfaces

### `TSLiteralType`

<details><summary>Interface Code</summary>

```ts
export interface TSLiteralType extends BaseNode {
  type: AST_NODE_TYPES.TSLiteralType;
  literal: LiteralExpression | UnaryExpression | UpdateExpression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSLiteralType` | ✗ |  |
| `literal` | `LiteralExpression | UnaryExpression | UpdateExpression` | ✗ |  |


---