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
📂 **`packages/ast-spec/src/type/TSTypeReference/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TSTypeParameterInstantiation` | `../../special/TSTypeParameterInstantiation/spec` |
| `EntityName` | `../../unions/EntityName` |


---

## Interfaces

### `TSTypeReference`

<details><summary>Interface Code</summary>

```ts
export interface TSTypeReference extends BaseNode {
  type: AST_NODE_TYPES.TSTypeReference;
  typeArguments: TSTypeParameterInstantiation | undefined;
  typeName: EntityName;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSTypeReference` | ✗ |  |
| `typeArguments` | `TSTypeParameterInstantiation | undefined` | ✗ |  |
| `typeName` | `EntityName` | ✗ |  |


---