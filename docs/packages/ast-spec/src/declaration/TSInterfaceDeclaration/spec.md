[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/declaration/TSInterfaceDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `TSInterfaceBody` | `../../special/TSInterfaceBody/spec` |
| `TSInterfaceHeritage` | `../../special/TSInterfaceHeritage/spec` |
| `TSTypeParameterDeclaration` | `../../special/TSTypeParameterDeclaration/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSInterfaceDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface TSInterfaceDeclaration extends BaseNode {
  type: AST_NODE_TYPES.TSInterfaceDeclaration;
  /**
   * The body of the interface
   */
  body: TSInterfaceBody;
  /**
   * Whether the interface was `declare`d
   */
  declare: boolean;
  /**
   * The types this interface `extends`
   */
  extends: TSInterfaceHeritage[];
  /**
   * The name of this interface
   */
  id: Identifier;
  /**
   * The generic type parameters declared for the interface. Empty declaration
   * (`<>`) is different from no declaration.
   */
  typeParameters: TSTypeParameterDeclaration | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSInterfaceDeclaration` | ✗ |  |
| `body` | `TSInterfaceBody` | ✗ |  |
| `declare` | `boolean` | ✗ |  |
| `extends` | `TSInterfaceHeritage[]` | ✗ |  |
| `id` | `Identifier` | ✗ |  |
| `typeParameters` | `TSTypeParameterDeclaration | undefined` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---