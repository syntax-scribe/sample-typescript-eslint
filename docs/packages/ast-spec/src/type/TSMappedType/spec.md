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
📂 **`packages/ast-spec/src/type/TSMappedType/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `TSTypeParameter` | `../../special/TSTypeParameter/spec` |
| `TypeNode` | `../../unions/TypeNode` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSMappedType`

<details><summary>Interface Code</summary>

```ts
export interface TSMappedType extends BaseNode {
  type: AST_NODE_TYPES.TSMappedType;
  constraint: TypeNode;
  key: Identifier;
  nameType: TypeNode | null;
  optional: boolean | '+' | '-' | undefined;
  readonly: boolean | '+' | '-' | undefined;
  typeAnnotation: TypeNode | undefined;
  /** @deprecated Use {@link `constraint`} and {@link `key`} instead. */
  typeParameter: TSTypeParameter;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSMappedType` | ✗ |  |
| `constraint` | `TypeNode` | ✗ |  |
| `key` | `Identifier` | ✗ |  |
| `nameType` | `TypeNode | null` | ✗ |  |
| `optional` | `boolean | '+' | '-' | undefined` | ✗ |  |
| `readonly` | `boolean | '+' | '-' | undefined` | ✗ |  |
| `typeAnnotation` | `TypeNode | undefined` | ✗ |  |
| `typeParameter` | `TSTypeParameter` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---