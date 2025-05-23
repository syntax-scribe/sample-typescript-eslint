[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSFunctionSignatureBase.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 1
- **Type Aliases**: 0

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

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---