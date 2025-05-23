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
📂 **`packages/ast-spec/src/declaration/TSEnumDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TSEnumMember` | `../../element/TSEnumMember/spec` |
| `Identifier` | `../../expression/Identifier/spec` |
| `TSEnumBody` | `../../special/TSEnumBody/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSEnumDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface TSEnumDeclaration extends BaseNode {
  type: AST_NODE_TYPES.TSEnumDeclaration;
  /**
   * The body of the enum.
   */
  body: TSEnumBody;
  /**
   * Whether this is a `const` enum.
   * @example
   * ```ts
   * const enum Foo {}
   * ```
   */
  const: boolean;
  /**
   * Whether this is a `declare`d enum.
   * @example
   * ```ts
   * declare enum Foo {}
   * ```
   */
  declare: boolean;
  /**
   * The enum name.
   */
  id: Identifier;
  /**
   * The enum members.
   * @deprecated Use {@link body} instead.
   */
  members: TSEnumMember[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSEnumDeclaration` | ✗ |  |
| `body` | `TSEnumBody` | ✗ |  |
| `const` | `boolean` | ✗ |  |
| `declare` | `boolean` | ✗ |  |
| `id` | `Identifier` | ✗ |  |
| `members` | `TSEnumMember[]` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---