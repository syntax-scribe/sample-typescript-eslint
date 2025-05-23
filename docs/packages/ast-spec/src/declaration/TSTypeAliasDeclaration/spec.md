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
📂 **`packages/ast-spec/src/declaration/TSTypeAliasDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `TSTypeParameterDeclaration` | `../../special/TSTypeParameterDeclaration/spec` |
| `TypeNode` | `../../unions/TypeNode` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSTypeAliasDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface TSTypeAliasDeclaration extends BaseNode {
  type: AST_NODE_TYPES.TSTypeAliasDeclaration;
  /**
   * Whether the type was `declare`d.
   * @example
   * ```ts
   * declare type T = 1;
   * ```
   */
  declare: boolean;
  /**
   * The name of the type.
   */
  id: Identifier;
  /**
   * The "value" (type) of the declaration
   */
  typeAnnotation: TypeNode;
  /**
   * The generic type parameters declared for the type. Empty declaration
   * (`<>`) is different from no declaration.
   */
  typeParameters: TSTypeParameterDeclaration | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSTypeAliasDeclaration` | ✗ |  |
| `declare` | `boolean` | ✗ |  |
| `id` | `Identifier` | ✗ |  |
| `typeAnnotation` | `TypeNode` | ✗ |  |
| `typeParameters` | `TSTypeParameterDeclaration | undefined` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---