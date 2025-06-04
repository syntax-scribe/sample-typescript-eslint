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
📂 **`packages/ast-spec/src/type/TSIntersectionType/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TypeNode` | `../../unions/TypeNode` |


---

## Interfaces

### `TSIntersectionType`

<details><summary>Interface Code</summary>

```ts
export interface TSIntersectionType extends BaseNode {
  type: AST_NODE_TYPES.TSIntersectionType;
  types: TypeNode[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSIntersectionType` | ✗ |  |
| `types` | `TypeNode[]` | ✗ |  |


---