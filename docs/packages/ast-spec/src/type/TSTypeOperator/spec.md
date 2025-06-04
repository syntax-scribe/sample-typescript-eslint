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
📂 **`packages/ast-spec/src/type/TSTypeOperator/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TypeNode` | `../../unions/TypeNode` |


---

## Interfaces

### `TSTypeOperator`

<details><summary>Interface Code</summary>

```ts
export interface TSTypeOperator extends BaseNode {
  type: AST_NODE_TYPES.TSTypeOperator;
  operator: 'keyof' | 'readonly' | 'unique';
  typeAnnotation: TypeNode | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSTypeOperator` | ✗ |  |
| `operator` | `'keyof' | 'readonly' | 'unique'` | ✗ |  |
| `typeAnnotation` | `TypeNode | undefined` | ✗ |  |


---