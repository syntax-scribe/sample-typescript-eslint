[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 1
- **Type Aliases**: 0

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

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---