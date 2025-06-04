[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `triple-slash-reference.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 4 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/triple-slash-reference.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `programNode` | `TSESTree.Node | undefined` | let/var | `*not shown*` | ✗ |
| `references` | `{
      comment: TSESTree.Comment;
      importName: string;
    }[]` | const | `[]` | ✗ |
| `referenceRegExp` | `RegExp` | const | `/^\/\s*<reference\s*(types|path|lib)\s*=\s*["|'](.*)["|']/` | ✗ |
| `reference` | `any` | const | `node.moduleReference` | ✗ |


---

## Functions

### `hasMatchingReference(source: TSESTree.Literal): void`

<details><summary>Code</summary>

```ts
function hasMatchingReference(source: TSESTree.Literal): void {
      references.forEach(reference => {
        if (reference.importName === source.value) {
          context.report({
            node: reference.comment,
            messageId: 'tripleSlashReference',
            data: {
              module: reference.importName,
            },
          });
        }
      });
    }
```
</details>

- **Parameters**:
  - `source: TSESTree.Literal`
- **Return Type**: `void`
- **Calls**:
  - `references.forEach`
  - `context.report`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    lib?: 'always' | 'never';
    path?: 'always' | 'never';
    types?: 'always' | 'never' | 'prefer-import';
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'tripleSlashReference';
```


---