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
📂 **`packages/ast-spec/src/expression/MetaProperty/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../Identifier/spec` |


---

## Interfaces

### `MetaProperty`

<details><summary>Interface Code</summary>

```ts
export interface MetaProperty extends BaseNode {
  type: AST_NODE_TYPES.MetaProperty;
  meta: Identifier;
  property: Identifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.MetaProperty` | ✗ |  |
| `meta` | `Identifier` | ✗ |  |
| `property` | `Identifier` | ✗ |  |


---