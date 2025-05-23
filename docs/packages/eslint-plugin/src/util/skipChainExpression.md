[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `skipChainExpression.ts`

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
📂 **`packages/eslint-plugin/src/util/skipChainExpression.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Functions

### `skipChainExpression(node: T): T | TSESTree.ChainElement`

<details><summary>Code</summary>

```ts
export function skipChainExpression<T extends TSESTree.Node>(
  node: T,
): T | TSESTree.ChainElement {
  return node.type === AST_NODE_TYPES.ChainExpression ? node.expression : node;
}
```
</details>

- **Parameters**:
  - `node: T`
- **Return Type**: `T | TSESTree.ChainElement`

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