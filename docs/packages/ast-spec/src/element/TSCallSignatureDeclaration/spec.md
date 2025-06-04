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
📂 **`packages/ast-spec/src/element/TSCallSignatureDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `TSFunctionSignatureBase` | `../../base/TSFunctionSignatureBase` |


---

## Interfaces

### `TSCallSignatureDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface TSCallSignatureDeclaration extends TSFunctionSignatureBase {
  type: AST_NODE_TYPES.TSCallSignatureDeclaration;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSCallSignatureDeclaration` | ✗ |  |


---