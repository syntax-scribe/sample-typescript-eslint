[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `triple-slash-reference.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 2

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