[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/declaration/TSImportEqualsDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `TSExternalModuleReference` | `../../special/TSExternalModuleReference/spec` |
| `TSQualifiedName` | `../../type/TSQualifiedName/spec` |
| `ImportKind` | `../ExportAndImportKind` |


---

## 🔧 Functions

> No functions found in this file.


---

## Interfaces

### `TSImportEqualsDeclarationBase`

<details><summary>Interface Code</summary>

```ts
interface TSImportEqualsDeclarationBase extends BaseNode {
  type: AST_NODE_TYPES.TSImportEqualsDeclaration;
  /**
   * The locally imported name.
   */
  id: Identifier;
  /**
   * The kind of the import. Always `'value'` unless `moduleReference` is a
   * `TSExternalModuleReference`.
   */
  importKind: ImportKind;
  /**
   * The value being aliased.
   * @example
   * ```ts
   * import F1 = A;
   * import F2 = A.B.C;
   * import F3 = require('mod');
   * ```
   */
  moduleReference: Identifier | TSExternalModuleReference | TSQualifiedName;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSImportEqualsDeclaration` | ✗ |  |
| `id` | `Identifier` | ✗ |  |
| `importKind` | `ImportKind` | ✗ |  |
| `moduleReference` | `Identifier | TSExternalModuleReference | TSQualifiedName` | ✗ |  |

### `TSImportEqualsNamespaceDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface TSImportEqualsNamespaceDeclaration
  extends TSImportEqualsDeclarationBase {
  /**
   * The kind of the import.
   */
  importKind: 'value';
  /**
   * The value being aliased.
   * ```
   * import F1 = A;
   * import F2 = A.B.C;
   * ```
   */
  moduleReference: Identifier | TSQualifiedName;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `importKind` | `'value'` | ✗ |  |
| `moduleReference` | `Identifier | TSQualifiedName` | ✗ |  |

### `TSImportEqualsRequireDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface TSImportEqualsRequireDeclaration
  extends TSImportEqualsDeclarationBase {
  /**
   * The kind of the import.
   */
  importKind: ImportKind;
  /**
   * The value being aliased.
   * ```
   * import F3 = require('mod');
   * ```
   */
  moduleReference: TSExternalModuleReference;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `importKind` | `ImportKind` | ✗ |  |
| `moduleReference` | `TSExternalModuleReference` | ✗ |  |


---

## Type Aliases

### `TSImportEqualsDeclaration`

```ts
type TSImportEqualsDeclaration = | TSImportEqualsNamespaceDeclaration
  | TSImportEqualsRequireDeclaration;
```


---