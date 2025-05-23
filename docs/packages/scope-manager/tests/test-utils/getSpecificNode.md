[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getSpecificNode.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/test-utils/getSpecificNode.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `TSESTree` | `@typescript-eslint/types` |
| `simpleTraverse` | `@typescript-eslint/typescript-estree` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---