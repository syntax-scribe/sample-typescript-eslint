[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/UpdateExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `UnaryExpressionBase` | `../../base/UnaryExpressionBase` |


---

## Interfaces

### `UpdateExpression`

<details><summary>Interface Code</summary>

```ts
export interface UpdateExpression extends UnaryExpressionBase {
  type: AST_NODE_TYPES.UpdateExpression;
  operator: '++' | '--';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.UpdateExpression` | ✗ |  |
| `operator` | `'++' | '--'` | ✗ |  |


---