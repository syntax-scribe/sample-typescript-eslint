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
📂 **`packages/ast-spec/src/type/TSTypePredicate/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `TSTypeAnnotation` | `../../special/TSTypeAnnotation/spec` |
| `TSThisType` | `../TSThisType/spec` |


---

## Interfaces

### `TSTypePredicate`

<details><summary>Interface Code</summary>

```ts
export interface TSTypePredicate extends BaseNode {
  type: AST_NODE_TYPES.TSTypePredicate;
  asserts: boolean;
  parameterName: Identifier | TSThisType;
  typeAnnotation: TSTypeAnnotation | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSTypePredicate` | ✗ |  |
| `asserts` | `boolean` | ✗ |  |
| `parameterName` | `Identifier | TSThisType` | ✗ |  |
| `typeAnnotation` | `TSTypeAnnotation | null` | ✗ |  |


---