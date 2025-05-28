[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getThisExpression.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

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