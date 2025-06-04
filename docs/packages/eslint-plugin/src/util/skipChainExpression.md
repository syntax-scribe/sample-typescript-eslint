[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `skipChainExpression.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

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