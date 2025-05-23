[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getThisExpression.ts`

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
📂 **`packages/eslint-plugin/src/util/getThisExpression.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Functions

### `getThisExpression(node: TSESTree.Node): TSESTree.ThisExpression | undefined`

<details><summary>Code</summary>

```ts
export function getThisExpression(
  node: TSESTree.Node,
): TSESTree.ThisExpression | undefined {
  while (true) {
    if (node.type === AST_NODE_TYPES.CallExpression) {
      node = node.callee;
    } else if (node.type === AST_NODE_TYPES.ThisExpression) {
      return node;
    } else if (node.type === AST_NODE_TYPES.MemberExpression) {
      node = node.object;
    } else if (node.type === AST_NODE_TYPES.ChainExpression) {
      node = node.expression;
    } else {
      break;
    }
  }

  return;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `TSESTree.ThisExpression | undefined`

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