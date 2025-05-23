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
📂 **`packages/ast-spec/src/declaration/ExportDefaultDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `DefaultExportDeclarations` | `../../unions/ExportDeclaration` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ExportDefaultDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface ExportDefaultDeclaration extends BaseNode {
  type: AST_NODE_TYPES.ExportDefaultDeclaration;
  /**
   * The declaration being exported.
   */
  declaration: DefaultExportDeclarations;
  /**
   * The kind of the export. Always `value` for default exports.
   */
  exportKind: 'value';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ExportDefaultDeclaration` | ✗ |  |
| `declaration` | `DefaultExportDeclarations` | ✗ |  |
| `exportKind` | `'value'` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---