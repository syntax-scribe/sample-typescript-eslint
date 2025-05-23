[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isStartOfExpressionStatement.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/isStartOfExpressionStatement.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Functions

### `isStartOfExpressionStatement(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
export function isStartOfExpressionStatement(node: TSESTree.Node): boolean {
  const start = node.range[0];
  let ancestor: TSESTree.Node | undefined = node;

  while ((ancestor = ancestor.parent) && ancestor.range[0] === start) {
    if (ancestor.type === AST_NODE_TYPES.ExpressionStatement) {
      return true;
    }
  }
  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Tests if a node appears at the beginning of an ancestor ExpressionStatement node.
 * @param node The node to check.
 * @returns Whether the node appears at the beginning of an ancestor ExpressionStatement node.
 */
```

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

> No type aliases found in this file.


---