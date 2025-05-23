[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-namespace.ts`

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
📂 **`packages/eslint-plugin/src/rules/no-namespace.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `isDefinitionFile` | `../util` |


---

## Functions

### `isDeclaration(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isDeclaration(node: TSESTree.Node): boolean {
      if (node.type === AST_NODE_TYPES.TSModuleDeclaration && node.declare) {
        return true;
      }

      return node.parent != null && isDeclaration(node.parent);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isDeclaration`

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
    allowDeclarations?: boolean;
    allowDefinitionFiles?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'moduleSyntaxIsPreferred';
```


---