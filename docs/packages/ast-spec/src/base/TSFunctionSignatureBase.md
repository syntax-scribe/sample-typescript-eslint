[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSFunctionSignatureBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/TSFunctionSignatureBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSTypeAnnotation` | `../special/TSTypeAnnotation/spec` |
| `TSTypeParameterDeclaration` | `../special/TSTypeParameterDeclaration/spec` |
| `Parameter` | `../unions/Parameter` |
| `BaseNode` | `./BaseNode` |


---

## Interfaces

### `TSFunctionSignatureBase`

<details><summary>Interface Code</summary>

```ts
export interface TSFunctionSignatureBase extends BaseNode {
  params: Parameter[];
  returnType: TSTypeAnnotation | undefined;
  typeParameters: TSTypeParameterDeclaration | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `params` | `Parameter[]` | ✗ |  |
| `returnType` | `TSTypeAnnotation | undefined` | ✗ |  |
| `typeParameters` | `TSTypeParameterDeclaration | undefined` | ✗ |  |


---