[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 6 |
| 🔄 Re-exports | 1 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Re-exports](#re-exports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/BinaryExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `PrivateIdentifier` | `../../special/PrivateIdentifier/spec` |
| `Expression` | `../../unions/Expression` |
| `ValueOf` | `../../utils` |
| `BinaryOperatorToText` | `./BinaryOperatorToText` |


---

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| namespace | `./BinaryOperatorToText` | * |


---

## Interfaces

### `BinaryExpression`

<details><summary>Interface Code</summary>

```ts
export interface BinaryExpression extends BaseNode {
  type: AST_NODE_TYPES.BinaryExpression;
  left: Expression | PrivateIdentifier;
  operator: ValueOf<BinaryOperatorToText>;
  right: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.BinaryExpression` | ✗ |  |
| `left` | `Expression | PrivateIdentifier` | ✗ |  |
| `operator` | `ValueOf<BinaryOperatorToText>` | ✗ |  |
| `right` | `Expression` | ✗ |  |


---