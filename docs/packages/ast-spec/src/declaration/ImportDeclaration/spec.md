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
📂 **`packages/ast-spec/src/declaration/ImportDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `StringLiteral` | `../../expression/literal/StringLiteral/spec` |
| `ImportAttribute` | `../../special/ImportAttribute/spec` |
| `ImportClause` | `../../unions/ImportClause` |
| `ImportKind` | `../ExportAndImportKind` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ImportDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface ImportDeclaration extends BaseNode {
  type: AST_NODE_TYPES.ImportDeclaration;
  /**
   * The assertions declared for the export.
   * @example
   * ```ts
   * import * from 'mod' assert \{ type: 'json' \};
   * ```
   * @deprecated Replaced with {@link `attributes`}.
   */
  assertions: ImportAttribute[];
  /**
   * The attributes declared for the export.
   * @example
   * ```ts
   * import * from 'mod' with \{ type: 'json' \};
   * ```
   */
  attributes: ImportAttribute[];
  /**
   * The kind of the import.
   */
  importKind: ImportKind;
  /**
   * The source module being imported from.
   */
  source: StringLiteral;
  /**
   * The specifiers being imported.
   * If this is an empty array then either there are no specifiers:
   * ```
   * import {} from 'mod';
   * ```
   * Or it is a side-effect import:
   * ```
   * import 'mod';
   * ```
   */
  specifiers: ImportClause[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ImportDeclaration` | ✗ |  |
| `assertions` | `ImportAttribute[]` | ✗ |  |
| `attributes` | `ImportAttribute[]` | ✗ |  |
| `importKind` | `ImportKind` | ✗ |  |
| `source` | `StringLiteral` | ✗ |  |
| `specifiers` | `ImportClause[]` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---