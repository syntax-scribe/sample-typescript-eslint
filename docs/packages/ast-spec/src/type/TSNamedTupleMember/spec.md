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
📂 **`packages/ast-spec/src/type/TSNamedTupleMember/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `TypeNode` | `../../unions/TypeNode` |


---

## Interfaces

### `TSNamedTupleMember`

<details><summary>Interface Code</summary>

```ts
export interface TSNamedTupleMember extends BaseNode {
  type: AST_NODE_TYPES.TSNamedTupleMember;
  elementType: TypeNode;
  label: Identifier;
  optional: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSNamedTupleMember` | ✗ |  |
| `elementType` | `TypeNode` | ✗ |  |
| `label` | `Identifier` | ✗ |  |
| `optional` | `boolean` | ✗ |  |


---