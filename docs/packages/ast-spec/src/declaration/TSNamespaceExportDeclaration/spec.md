[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/declaration/TSNamespaceExportDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSNamespaceExportDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface TSNamespaceExportDeclaration extends BaseNode {
  type: AST_NODE_TYPES.TSNamespaceExportDeclaration;
  /**
   * The name of the global variable that's exported as namespace
   */
  id: Identifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSNamespaceExportDeclaration` | ✗ |  |
| `id` | `Identifier` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---