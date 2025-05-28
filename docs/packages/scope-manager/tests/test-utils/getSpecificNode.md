[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getSpecificNode.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
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
📂 **`packages/scope-manager/tests/test-utils/getSpecificNode.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `TSESTree` | `@typescript-eslint/types` |
| `simpleTraverse` | `@typescript-eslint/typescript-estree` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `node` | `TSESTree.Node | null | undefined` | let/var | `null` | ✗ |
| `res` | `any` | const | `cb ? cb(n) : n` | ✗ |


---

## Functions

### `getSpecificNode(ast: TSESTree.Node, selector: Selector, cb: (node: Node) => boolean | null | undefined): Node`

<details><summary>Code</summary>

```ts
export function getSpecificNode<
  Selector extends AST_NODE_TYPES,
  Node extends Extract<TSESTree.Node, { type: Selector }>,
>(
  ast: TSESTree.Node,
  selector: Selector,
  cb?: (node: Node) => boolean | null | undefined,
): Node;
```
</details>

- **Parameters**:
  - `ast: TSESTree.Node`
  - `selector: Selector`
  - `cb: (node: Node) => boolean | null | undefined`
- **Return Type**: `Node`

---