[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-useless-empty-export.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 6
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---