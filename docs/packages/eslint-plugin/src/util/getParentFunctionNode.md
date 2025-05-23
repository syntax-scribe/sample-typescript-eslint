[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getParentFunctionNode.ts`

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
📂 **`packages/eslint-plugin/src/util/getParentFunctionNode.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Functions

### `getParentFunctionNode(node: TSESTree.Node): | TSESTree.ArrowFunctionExpression
  | TSESTree.FunctionDeclaration
  | TSESTree.FunctionExpression
  | null`

<details><summary>Code</summary>

```ts
export function getParentFunctionNode(
  node: TSESTree.Node,
):
  | TSESTree.ArrowFunctionExpression
  | TSESTree.FunctionDeclaration
  | TSESTree.FunctionExpression
  | null {
  let current = node.parent;
  while (current) {
    if (
      current.type === AST_NODE_TYPES.ArrowFunctionExpression ||
      current.type === AST_NODE_TYPES.FunctionDeclaration ||
      current.type === AST_NODE_TYPES.FunctionExpression
    ) {
      return current;
    }

    current = current.parent;
  }

  // this shouldn't happen in correct code, but someone may attempt to parse bad code
  // the parser won't error, so we shouldn't throw here
  /* istanbul ignore next */ return null;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `| TSESTree.ArrowFunctionExpression
  | TSESTree.FunctionDeclaration
  | TSESTree.FunctionExpression
  | null`
- **Internal Comments**:
```
// this shouldn't happen in correct code, but someone may attempt to parse bad code
// the parser won't error, so we shouldn't throw here
/* istanbul ignore next */
```


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