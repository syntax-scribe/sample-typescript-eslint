[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/special/ExportSpecifier/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `ExportKind` | `../../declaration/ExportAndImportKind` |
| `Identifier` | `../../expression/Identifier/spec` |
| `StringLiteral` | `../../expression/literal/StringLiteral/spec` |


---

## Interfaces

### `ExportSpecifierBase`

<details><summary>Interface Code</summary>

```ts
interface ExportSpecifierBase extends BaseNode {
  type: AST_NODE_TYPES.ExportSpecifier;
  exported: Identifier | StringLiteral;
  exportKind: ExportKind;
  local: Identifier | StringLiteral;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ExportSpecifier` | ✗ |  |
| `exported` | `Identifier | StringLiteral` | ✗ |  |
| `exportKind` | `ExportKind` | ✗ |  |
| `local` | `Identifier | StringLiteral` | ✗ |  |

### `ExportSpecifierWithIdentifierLocal`

<details><summary>Interface Code</summary>

```ts
export interface ExportSpecifierWithIdentifierLocal
  extends ExportSpecifierBase {
  local: Identifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `local` | `Identifier` | ✗ |  |

### `ExportSpecifierWithStringOrLiteralLocal`

<details><summary>Interface Code</summary>

```ts
export interface ExportSpecifierWithStringOrLiteralLocal
  extends ExportSpecifierBase {
  local: Identifier | StringLiteral;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `local` | `Identifier | StringLiteral` | ✗ |  |


---

## Type Aliases

### `ExportSpecifier`

```ts
type ExportSpecifier = | ExportSpecifierWithIdentifierLocal
  | ExportSpecifierWithStringOrLiteralLocal;
```


---