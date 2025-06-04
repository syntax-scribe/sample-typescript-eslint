[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-useless-empty-export.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-useless-empty-export.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `isDefinitionFile` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `exportOrImportNodeTypes` | `Set<any>` | const | `new Set([
  AST_NODE_TYPES.ExportAllDeclaration,
  AST_NODE_TYPES.ExportDefaultDeclaration,
  AST_NODE_TYPES.ExportNamedDeclaration,
  AST_NODE_TYPES.ExportSpecifier,
  AST_NODE_TYPES.ImportDeclaration,
  AST_NODE_TYPES.TSExportAssignment,
  AST_NODE_TYPES.TSImportEqualsDeclaration,
])` | ✗ |
| `emptyExports` | `TSESTree.ExportNamedDeclaration[]` | const | `[]` | ✗ |
| `foundOtherExport` | `boolean` | let/var | `false` | ✗ |


---

## Functions

### `isEmptyExport(node: TSESTree.Node): node is TSESTree.ExportNamedDeclaration`

<details><summary>Code</summary>

```ts
function isEmptyExport(
  node: TSESTree.Node,
): node is TSESTree.ExportNamedDeclaration {
  return (
    node.type === AST_NODE_TYPES.ExportNamedDeclaration &&
    node.specifiers.length === 0 &&
    !node.declaration
  );
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.ExportNamedDeclaration`
### `checkNode(node: TSESTree.Program | TSESTree.TSModuleDeclaration): void`

<details><summary>Code</summary>

```ts
function checkNode(
      node: TSESTree.Program | TSESTree.TSModuleDeclaration,
    ): void {
      if (!Array.isArray(node.body)) {
        return;
      }

      const emptyExports: TSESTree.ExportNamedDeclaration[] = [];
      let foundOtherExport = false;

      for (const statement of node.body) {
        if (isEmptyExport(statement)) {
          emptyExports.push(statement);
        } else if (exportOrImportNodeTypes.has(statement.type)) {
          foundOtherExport = true;
        }
      }

      if (foundOtherExport) {
        for (const emptyExport of emptyExports) {
          context.report({
            node: emptyExport,
            messageId: 'uselessExport',
            fix: fixer => fixer.remove(emptyExport),
          });
        }
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Program | TSESTree.TSModuleDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `Array.isArray`
  - `isEmptyExport`
  - `emptyExports.push`
  - `exportOrImportNodeTypes.has`
  - `context.report`
  - `fixer.remove`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.remove(emptyExport)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.remove(emptyExport)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.remove(emptyExport)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.remove(emptyExport)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.remove`

---