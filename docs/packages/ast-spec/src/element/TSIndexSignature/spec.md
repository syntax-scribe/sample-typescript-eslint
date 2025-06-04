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