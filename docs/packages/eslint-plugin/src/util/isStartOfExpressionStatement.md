[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isStartOfExpressionStatement.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 2 |
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
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/isStartOfExpressionStatement.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `start` | `any` | const | `node.range[0]` | ✗ |
| `ancestor` | `TSESTree.Node | undefined` | let/var | `node` | ✗ |


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