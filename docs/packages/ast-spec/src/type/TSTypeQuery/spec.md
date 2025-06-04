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
📂 **`packages/ast-spec/src/type/TSTypeQuery/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TSTypeParameterInstantiation` | `../../special/spec` |
| `EntityName` | `../../unions/EntityName` |
| `TSImportType` | `../TSImportType/spec` |


---

## Interfaces

### `TSTypeQuery`

<details><summary>Interface Code</summary>

```ts
export interface TSTypeQuery extends BaseNode {
  type: AST_NODE_TYPES.TSTypeQuery;
  exprName: EntityName | TSImportType;
  typeArguments: TSTypeParameterInstantiation | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSTypeQuery` | ✗ |  |
| `exprName` | `EntityName | TSImportType` | ✗ |  |
| `typeArguments` | `TSTypeParameterInstantiation | undefined` | ✗ |  |


---