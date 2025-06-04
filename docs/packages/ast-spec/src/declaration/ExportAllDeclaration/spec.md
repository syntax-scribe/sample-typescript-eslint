[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 6 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/declaration/ExportAllDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `StringLiteral` | `../../expression/literal/StringLiteral/spec` |
| `ImportAttribute` | `../../special/ImportAttribute/spec` |
| `ExportKind` | `../ExportAndImportKind` |


---

## Interfaces

### `ExportAllDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface ExportAllDeclaration extends BaseNode {
  type: AST_NODE_TYPES.ExportAllDeclaration;
  /**
   * The assertions declared for the export.
   * @example
   * ```ts
   * export * from 'mod' assert \{ type: 'json' \};
   * ```
   * @deprecated Replaced with {@link `attributes`}.
   */
  assertions: ImportAttribute[];
  /**
   * The attributes declared for the export.
   * @example
   * ```ts
   * export * from 'mod' with \{ type: 'json' \};
   * ```
   */
  attributes: ImportAttribute[];
  /**
   * The name for the exported items (`as X`). `null` if no name is assigned.
   */
  exported: Identifier | null;
  /**
   * The kind of the export.
   */
  exportKind: ExportKind;
  /**
   * The source module being exported from.
   */
  source: StringLiteral;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ExportAllDeclaration` | ✗ |  |
| `assertions` | `ImportAttribute[]` | ✗ |  |
| `attributes` | `ImportAttribute[]` | ✗ |  |
| `exported` | `Identifier | null` | ✗ |  |
| `exportKind` | `ExportKind` | ✗ |  |
| `source` | `StringLiteral` | ✗ |  |


---