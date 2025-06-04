[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 🔄 Re-exports | 1 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Re-exports](#re-exports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/AssignmentExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |
| `ValueOf` | `../../utils` |
| `AssignmentOperatorToText` | `./AssignmentOperatorToText` |


---

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| namespace | `./AssignmentOperatorToText` | * |


---

## Interfaces

### `AssignmentExpression`

<details><summary>Interface Code</summary>

```ts
export interface AssignmentExpression extends BaseNode {
  type: AST_NODE_TYPES.AssignmentExpression;
  left: Expression;
  operator: ValueOf<AssignmentOperatorToText>;
  right: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.AssignmentExpression` | ✗ |  |
| `left` | `Expression` | ✗ |  |
| `operator` | `ValueOf<AssignmentOperatorToText>` | ✗ |  |
| `right` | `Expression` | ✗ |  |


---