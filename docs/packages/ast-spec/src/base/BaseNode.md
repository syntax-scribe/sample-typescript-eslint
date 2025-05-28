[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `BaseNode.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/BaseNode.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../ast-node-types` |
| `NodeOrTokenData` | `./NodeOrTokenData` |


---

## 🔧 Functions

> No functions found in this file.


---

## Interfaces

### `BaseNode`

<details><summary>Interface Code</summary>

```ts
export interface BaseNode extends NodeOrTokenData {
  type: AST_NODE_TYPES;

  /**
   * The parent node of the current node
   *
   * This is added in the @typescript-eslint/types package as ESLint adds it
   * while traversing.
   */
  // parent?: Node;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES` | ✗ |  |


---