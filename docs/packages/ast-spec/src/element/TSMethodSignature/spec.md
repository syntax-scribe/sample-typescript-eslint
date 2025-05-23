[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 9
- **Interfaces**: 3
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/ast-spec/src/element/TSMethodSignature/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `Accessibility` | `../../base/Accessibility` |
| `BaseNode` | `../../base/BaseNode` |
| `TSTypeAnnotation` | `../../special/TSTypeAnnotation/spec` |
| `TSTypeParameterDeclaration` | `../../special/TSTypeParameterDeclaration/spec` |
| `Parameter` | `../../unions/Parameter` |
| `PropertyName` | `../../unions/PropertyName` |
| `PropertyNameComputed` | `../../unions/PropertyName` |
| `PropertyNameNonComputed` | `../../unions/PropertyName` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSMethodSignatureBase`

<details><summary>Interface Code</summary>

```ts
interface TSMethodSignatureBase extends BaseNode {
  type: AST_NODE_TYPES.TSMethodSignature;
  accessibility: Accessibility | undefined;
  computed: boolean;
  key: PropertyName;
  kind: 'get' | 'method' | 'set';
  optional: boolean;
  params: Parameter[];
  readonly: boolean;
  returnType: TSTypeAnnotation | undefined;
  static: boolean;
  typeParameters: TSTypeParameterDeclaration | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSMethodSignature` | ✗ |  |
| `accessibility` | `Accessibility | undefined` | ✗ |  |
| `computed` | `boolean` | ✗ |  |
| `key` | `PropertyName` | ✗ |  |
| `kind` | `'get' | 'method' | 'set'` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `params` | `Parameter[]` | ✗ |  |
| `readonly` | `boolean` | ✗ |  |
| `returnType` | `TSTypeAnnotation | undefined` | ✗ |  |
| `static` | `boolean` | ✗ |  |
| `typeParameters` | `TSTypeParameterDeclaration | undefined` | ✗ |  |

### `TSMethodSignatureComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSMethodSignatureComputedName extends TSMethodSignatureBase {
  computed: true;
  key: PropertyNameComputed;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `computed` | `true` | ✗ |  |
| `key` | `PropertyNameComputed` | ✗ |  |

### `TSMethodSignatureNonComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSMethodSignatureNonComputedName
  extends TSMethodSignatureBase {
  computed: false;
  key: PropertyNameNonComputed;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `computed` | `false` | ✗ |  |
| `key` | `PropertyNameNonComputed` | ✗ |  |


---

## Type Aliases

### `TSMethodSignature`

```ts
type TSMethodSignature = | TSMethodSignatureComputedName
  | TSMethodSignatureNonComputedName;
```


---