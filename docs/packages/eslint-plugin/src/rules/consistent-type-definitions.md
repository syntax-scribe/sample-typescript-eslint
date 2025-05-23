[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `consistent-type-definitions.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/consistent-type-definitions.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Functions

### `isCurrentlyTraversedNodeWithinModuleDeclaration(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isCurrentlyTraversedNodeWithinModuleDeclaration(
      node: TSESTree.Node,
    ): boolean {
      return context.sourceCode
        .getAncestors(node)
        .some(
          node =>
            node.type === AST_NODE_TYPES.TSModuleDeclaration &&
            node.declare &&
            node.kind === 'global',
        );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Iterates from the highest parent to the currently traversed node
     * to determine whether any node in tree is globally declared module declaration
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode
        .getAncestors(node)
        .some`

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