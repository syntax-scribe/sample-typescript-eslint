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
📂 **`packages/ast-spec/src/special/ImportSpecifier/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `ImportKind` | `../../declaration/ExportAndImportKind` |
| `Identifier` | `../../expression/Identifier/spec` |
| `StringLiteral` | `../../expression/literal/StringLiteral/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ImportSpecifier`

<details><summary>Interface Code</summary>

```ts
export interface ImportSpecifier extends BaseNode {
  type: AST_NODE_TYPES.ImportSpecifier;
  imported: Identifier | StringLiteral;
  importKind: ImportKind;
  local: Identifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ImportSpecifier` | ✗ |  |
| `imported` | `Identifier | StringLiteral` | ✗ |  |
| `importKind` | `ImportKind` | ✗ |  |
| `local` | `Identifier` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---