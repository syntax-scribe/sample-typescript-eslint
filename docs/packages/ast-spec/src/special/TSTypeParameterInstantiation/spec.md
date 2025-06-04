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
📂 **`packages/ast-spec/src/special/TSTypeParameterInstantiation/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TypeNode` | `../../unions/TypeNode` |


---

## Interfaces

### `TSTypeParameterInstantiation`

<details><summary>Interface Code</summary>

```ts
export interface TSTypeParameterInstantiation extends BaseNode {
  type: AST_NODE_TYPES.TSTypeParameterInstantiation;
  params: TypeNode[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSTypeParameterInstantiation` | ✗ |  |
| `params` | `TypeNode[]` | ✗ |  |


---