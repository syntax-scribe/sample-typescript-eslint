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