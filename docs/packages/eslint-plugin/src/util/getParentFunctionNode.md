[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getParentFunctionNode.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 1 |
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
📂 **`packages/eslint-plugin/src/util/getParentFunctionNode.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `current` | `any` | let/var | `node.parent` | ✗ |


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