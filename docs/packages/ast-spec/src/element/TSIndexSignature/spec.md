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
📂 **`packages/ast-spec/src/element/TSIndexSignature/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `Accessibility` | `../../base/Accessibility` |
| `BaseNode` | `../../base/BaseNode` |
| `TSTypeAnnotation` | `../../special/TSTypeAnnotation/spec` |
| `Parameter` | `../../unions/Parameter` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSIndexSignature`

<details><summary>Interface Code</summary>

```ts
export interface TSIndexSignature extends BaseNode {
  type: AST_NODE_TYPES.TSIndexSignature;
  accessibility: Accessibility | undefined;
  parameters: Parameter[];
  readonly: boolean;
  static: boolean;
  typeAnnotation: TSTypeAnnotation | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSIndexSignature` | ✗ |  |
| `accessibility` | `Accessibility | undefined` | ✗ |  |
| `parameters` | `Parameter[]` | ✗ |  |
| `readonly` | `boolean` | ✗ |  |
| `static` | `boolean` | ✗ |  |
| `typeAnnotation` | `TSTypeAnnotation | undefined` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---