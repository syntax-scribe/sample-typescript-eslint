[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/type/TSFunctionType/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `TSFunctionSignatureBase` | `../../base/TSFunctionSignatureBase` |


---

## Interfaces

### `TSFunctionType`

<details><summary>Interface Code</summary>

```ts
export interface TSFunctionType extends TSFunctionSignatureBase {
  type: AST_NODE_TYPES.TSFunctionType;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSFunctionType` | ✗ |  |


---