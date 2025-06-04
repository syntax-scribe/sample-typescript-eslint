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
📂 **`packages/ast-spec/src/expression/TSInstantiationExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TSTypeParameterInstantiation` | `../../special/spec` |
| `Expression` | `../../unions/Expression` |


---

## Interfaces

### `TSInstantiationExpression`

<details><summary>Interface Code</summary>

```ts
export interface TSInstantiationExpression extends BaseNode {
  type: AST_NODE_TYPES.TSInstantiationExpression;
  expression: Expression;
  typeArguments: TSTypeParameterInstantiation;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSInstantiationExpression` | ✗ |  |
| `expression` | `Expression` | ✗ |  |
| `typeArguments` | `TSTypeParameterInstantiation` | ✗ |  |


---