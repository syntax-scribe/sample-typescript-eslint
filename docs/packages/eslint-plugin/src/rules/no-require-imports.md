[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-require-imports.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-require-imports.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ASTUtils` | `@typescript-eslint/utils` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


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