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
📂 **`packages/ast-spec/src/expression/CallExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TSTypeParameterInstantiation` | `../../special/TSTypeParameterInstantiation/spec` |
| `CallExpressionArgument` | `../../unions/CallExpressionArgument` |
| `Expression` | `../../unions/Expression` |


---

## Interfaces

### `CallExpression`

<details><summary>Interface Code</summary>

```ts
export interface CallExpression extends BaseNode {
  type: AST_NODE_TYPES.CallExpression;
  arguments: CallExpressionArgument[];
  callee: Expression;
  optional: boolean;
  typeArguments: TSTypeParameterInstantiation | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.CallExpression` | ✗ |  |
| `arguments` | `CallExpressionArgument[]` | ✗ |  |
| `callee` | `Expression` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `typeArguments` | `TSTypeParameterInstantiation | undefined` | ✗ |  |


---