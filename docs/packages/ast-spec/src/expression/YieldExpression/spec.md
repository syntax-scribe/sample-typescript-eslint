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
📂 **`packages/ast-spec/src/expression/YieldExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |


---

## Interfaces

### `YieldExpression`

<details><summary>Interface Code</summary>

```ts
export interface YieldExpression extends BaseNode {
  type: AST_NODE_TYPES.YieldExpression;
  argument: Expression | null;
  delegate: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.YieldExpression` | ✗ |  |
| `argument` | `Expression | null` | ✗ |  |
| `delegate` | `boolean` | ✗ |  |


---