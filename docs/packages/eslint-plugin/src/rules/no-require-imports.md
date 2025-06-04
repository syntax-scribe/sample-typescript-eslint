[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-require-imports.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 1 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-require-imports.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ASTUtils` | `@typescript-eslint/utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `allowAsImport` | `any` | const | `options[0].allowAsImport` | ✗ |


---

## Functions

### `isImportPathAllowed(importPath: string): boolean | undefined`

<details><summary>Code</summary>

```ts
function isImportPathAllowed(importPath: string): boolean | undefined {
      return allowPatterns?.some(pattern => importPath.match(pattern));
    }
```
</details>

- **Parameters**:
  - `importPath: string`
- **Return Type**: `boolean | undefined`
- **Calls**:
  - `allowPatterns?.some`
  - `importPath.match`
### `isStringOrTemplateLiteral(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isStringOrTemplateLiteral(node: TSESTree.Node): boolean {
      return (
        (node.type === AST_NODE_TYPES.Literal &&
          typeof node.value === 'string') ||
        node.type === AST_NODE_TYPES.TemplateLiteral
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    allow?: string[];
    allowAsImport?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'noRequireImports';
```


---