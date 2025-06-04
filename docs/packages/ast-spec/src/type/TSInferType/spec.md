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
📂 **`packages/ast-spec/src/type/TSInferType/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TSTypeParameter` | `../../special/TSTypeParameter/spec` |


---

## Interfaces

### `TSInferType`

<details><summary>Interface Code</summary>

```ts
export interface TSInferType extends BaseNode {
  type: AST_NODE_TYPES.TSInferType;
  typeParameter: TSTypeParameter;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSInferType` | ✗ |  |
| `typeParameter` | `TSTypeParameter` | ✗ |  |


---