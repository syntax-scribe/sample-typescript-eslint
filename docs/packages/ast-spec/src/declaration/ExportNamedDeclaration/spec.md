[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 4
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/ast-spec/src/declaration/ExportNamedDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `StringLiteral` | `../../expression/literal/StringLiteral/spec` |
| `ExportSpecifier` | `../../special/ExportSpecifier/spec` |
| `ExportSpecifierWithIdentifierLocal` | `../../special/ExportSpecifier/spec` |
| `ImportAttribute` | `../../special/ImportAttribute/spec` |
| `NamedExportDeclarations` | `../../unions/ExportDeclaration` |
| `ExportKind` | `../ExportAndImportKind` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ExportNamedDeclarationBase`

<details><summary>Interface Code</summary>

```ts
interface ExportNamedDeclarationBase extends BaseNode {
  type: AST_NODE_TYPES.ExportNamedDeclaration;
  /**
   * The assertions declared for the export.
   * @example
   * ```ts
   * export { foo } from 'mod' assert \{ type: 'json' \};
   * ```
   * This will be an empty array if `source` is `null`
   * @deprecated Replaced with {@link `attributes`}.
   */
  assertions: ImportAttribute[];
  /**
   * The attributes declared for the export.
   * @example
   * ```ts
   * export { foo } from 'mod' with \{ type: 'json' \};
   * ```
   * This will be an empty array if `source` is `null`
   */
  attributes: ImportAttribute[];
  /**
   * The exported declaration.
   * @example
   * ```ts
   * export const x = 1;
   * ```
   * This will be `null` if `source` is not `null`, or if there are `specifiers`
   */
  declaration: NamedExportDeclarations | null;
  /**
   * The kind of the export.
   */
  exportKind: ExportKind;
  /**
   * The source module being exported from.
   */
  source: StringLiteral | null;
  /**
   * The specifiers being exported.
   * @example
   * ```ts
   * export { a, b };
   * ```
   * This will be an empty array if `declaration` is not `null`
   */
  specifiers: ExportSpecifier[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ExportNamedDeclaration` | ✗ |  |
| `assertions` | `ImportAttribute[]` | ✗ |  |
| `attributes` | `ImportAttribute[]` | ✗ |  |
| `declaration` | `NamedExportDeclarations | null` | ✗ |  |
| `exportKind` | `ExportKind` | ✗ |  |
| `source` | `StringLiteral | null` | ✗ |  |
| `specifiers` | `ExportSpecifier[]` | ✗ |  |

### `ExportNamedDeclarationWithoutSourceWithMultiple`

<details><summary>Interface Code</summary>

```ts
export interface ExportNamedDeclarationWithoutSourceWithMultiple
  extends ExportNamedDeclarationBase {
  /**
   * This will always be an empty array.
   * @deprecated Replaced with {@link `attributes`}.
   */
  assertions: ImportAttribute[];
  /**
   * This will always be an empty array.
   */
  attributes: ImportAttribute[];
  declaration: null;
  source: null;
  // Cannot have literal local without a source
  specifiers: ExportSpecifierWithIdentifierLocal[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `assertions` | `ImportAttribute[]` | ✗ |  |
| `attributes` | `ImportAttribute[]` | ✗ |  |
| `declaration` | `null` | ✗ |  |
| `source` | `null` | ✗ |  |
| `specifiers` | `ExportSpecifierWithIdentifierLocal[]` | ✗ |  |

### `ExportNamedDeclarationWithoutSourceWithSingle`

<details><summary>Interface Code</summary>

```ts
export interface ExportNamedDeclarationWithoutSourceWithSingle
  extends ExportNamedDeclarationBase {
  /**
   * This will always be an empty array.
   * @deprecated Replaced with {@link `attributes`}.
   */
  assertions: ImportAttribute[];
  /**
   * This will always be an empty array.
   */
  attributes: ImportAttribute[];
  declaration: NamedExportDeclarations;
  source: null;
  /**
   * This will always be an empty array.
   */
  specifiers: ExportSpecifierWithIdentifierLocal[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `assertions` | `ImportAttribute[]` | ✗ |  |
| `attributes` | `ImportAttribute[]` | ✗ |  |
| `declaration` | `NamedExportDeclarations` | ✗ |  |
| `source` | `null` | ✗ |  |
| `specifiers` | `ExportSpecifierWithIdentifierLocal[]` | ✗ |  |

### `ExportNamedDeclarationWithSource`

<details><summary>Interface Code</summary>

```ts
export interface ExportNamedDeclarationWithSource
  extends ExportNamedDeclarationBase {
  declaration: null;
  source: StringLiteral;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `declaration` | `null` | ✗ |  |
| `source` | `StringLiteral` | ✗ |  |


---

## Type Aliases

### `ExportNamedDeclarationWithoutSource`

```ts
type ExportNamedDeclarationWithoutSource = | ExportNamedDeclarationWithoutSourceWithMultiple
  | ExportNamedDeclarationWithoutSourceWithSingle;
```

### `ExportNamedDeclaration`

```ts
type ExportNamedDeclaration = | ExportNamedDeclarationWithoutSourceWithMultiple
  | ExportNamedDeclarationWithoutSourceWithSingle
  | ExportNamedDeclarationWithSource;
```


---