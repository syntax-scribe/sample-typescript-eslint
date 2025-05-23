[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `nodes.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 5
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/plugins/utils/nodes.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `MdxFlowExpression` | `mdast-util-mdx` |


---

## Functions

### `nodeIsCode(node: unist.Node): node is mdast.Code`

<details><summary>Code</summary>

```ts
export function nodeIsCode(node: unist.Node): node is mdast.Code {
  return node.type === 'code';
}
```
</details>

- **Parameters**:
  - `node: unist.Node`
- **Return Type**: `node is mdast.Code`
### `nodeIsHeading(node: unist.Node): node is mdast.Heading`

<details><summary>Code</summary>

```ts
export function nodeIsHeading(node: unist.Node): node is mdast.Heading {
  return node.type === 'heading';
}
```
</details>

- **Parameters**:
  - `node: unist.Node`
- **Return Type**: `node is mdast.Heading`
### `nodeIsParagraph(node: unist.Node): node is mdast.Paragraph`

<details><summary>Code</summary>

```ts
export function nodeIsParagraph(node: unist.Node): node is mdast.Paragraph {
  return node.type === 'paragraph';
}
```
</details>

- **Parameters**:
  - `node: unist.Node`
- **Return Type**: `node is mdast.Paragraph`
### `nodeIsMdxFlowExpression(node: unist.Node): node is MdxFlowExpression`

<details><summary>Code</summary>

```ts
export function nodeIsMdxFlowExpression(
  node: unist.Node,
): node is MdxFlowExpression {
  return node.type === 'mdxFlowExpression';
}
```
</details>

- **Parameters**:
  - `node: unist.Node`
- **Return Type**: `node is MdxFlowExpression`
### `nodeIsParent(node: unist.Node): node is unist.Parent`

<details><summary>Code</summary>

```ts
export function nodeIsParent(node: unist.Node): node is unist.Parent {
  return 'children' in node;
}
```
</details>

- **Parameters**:
  - `node: unist.Node`
- **Return Type**: `node is unist.Parent`

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