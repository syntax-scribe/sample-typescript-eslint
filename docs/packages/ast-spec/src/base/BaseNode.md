[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `BaseNode.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📐 Interfaces | 1 |

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