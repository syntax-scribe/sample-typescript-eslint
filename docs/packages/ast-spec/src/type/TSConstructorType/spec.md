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
📂 **`packages/ast-spec/src/type/TSConstructorType/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `TSFunctionSignatureBase` | `../../base/TSFunctionSignatureBase` |


---

## Interfaces

### `TSConstructorType`

<details><summary>Interface Code</summary>

```ts
export interface TSConstructorType extends TSFunctionSignatureBase {
  type: AST_NODE_TYPES.TSConstructorType;
  abstract: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSConstructorType` | ✗ |  |
| `abstract` | `boolean` | ✗ |  |


---