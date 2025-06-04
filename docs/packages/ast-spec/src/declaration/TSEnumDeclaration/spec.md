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