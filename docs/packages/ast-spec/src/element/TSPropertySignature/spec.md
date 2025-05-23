[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 3
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/ast-spec/src/element/TSPropertySignature/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `Accessibility` | `../../base/Accessibility` |
| `BaseNode` | `../../base/BaseNode` |
| `TSTypeAnnotation` | `../../special/TSTypeAnnotation/spec` |
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

### `TSPropertySignatureBase`

<details><summary>Interface Code</summary>

```ts
interface TSPropertySignatureBase extends BaseNode {
  type: AST_NODE_TYPES.TSPropertySignature;
  accessibility: Accessibility | undefined;
  computed: boolean;
  key: PropertyName;
  optional: boolean;
  readonly: boolean;
  static: boolean;
  typeAnnotation: TSTypeAnnotation | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSPropertySignature` | ✗ |  |
| `accessibility` | `Accessibility | undefined` | ✗ |  |
| `computed` | `boolean` | ✗ |  |
| `key` | `PropertyName` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `readonly` | `boolean` | ✗ |  |
| `static` | `boolean` | ✗ |  |
| `typeAnnotation` | `TSTypeAnnotation | undefined` | ✗ |  |

### `TSPropertySignatureComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSPropertySignatureComputedName
  extends TSPropertySignatureBase {
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

### `TSPropertySignatureNonComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSPropertySignatureNonComputedName
  extends TSPropertySignatureBase {
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

### `TSPropertySignature`

```ts
type TSPropertySignature = | TSPropertySignatureComputedName
  | TSPropertySignatureNonComputedName;
```


---