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
📂 **`packages/ast-spec/src/expression/TSAsExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |
| `TypeNode` | `../../unions/TypeNode` |


---

## Interfaces

### `TSAsExpression`

<details><summary>Interface Code</summary>

```ts
export interface TSAsExpression extends BaseNode {
  type: AST_NODE_TYPES.TSAsExpression;
  expression: Expression;
  typeAnnotation: TypeNode;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSAsExpression` | ✗ |  |
| `expression` | `Expression` | ✗ |  |
| `typeAnnotation` | `TypeNode` | ✗ |  |


---