[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-var-requires.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 1 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-var-requires.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ASTUtils` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getStaticStringValue` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `parent` | `any` | const | `node.parent.type === AST_NODE_TYPES.ChainExpression
            ? node.parent.parent
            : node.parent` | ✗ |


---

## Functions

### `isImportPathAllowed(importPath: string): boolean`

<details><summary>Code</summary>

```ts
function isImportPathAllowed(importPath: string): boolean {
      return allowPatterns.some(pattern => importPath.match(pattern));
    }
```
</details>

- **Parameters**:
  - `importPath: string`
- **Return Type**: `boolean`
- **Calls**:
  - `allowPatterns.some`
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
    allow: string[];
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'noVarReqs';
```


---