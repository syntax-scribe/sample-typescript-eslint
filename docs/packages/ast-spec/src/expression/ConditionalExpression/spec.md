[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/ConditionalExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |


---

## Interfaces

### `ConditionalExpression`

<details><summary>Interface Code</summary>

```ts
export interface ConditionalExpression extends BaseNode {
  type: AST_NODE_TYPES.ConditionalExpression;
  alternate: Expression;
  consequent: Expression;
  test: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ConditionalExpression` | ✗ |  |
| `alternate` | `Expression` | ✗ |  |
| `consequent` | `Expression` | ✗ |  |
| `test` | `Expression` | ✗ |  |


---