[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/JSXElement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `JSXClosingElement` | `../../jsx/JSXClosingElement/spec` |
| `JSXOpeningElement` | `../../jsx/JSXOpeningElement/spec` |
| `JSXChild` | `../../unions/JSXChild` |


---

## Interfaces

### `JSXElement`

<details><summary>Interface Code</summary>

```ts
export interface JSXElement extends BaseNode {
  type: AST_NODE_TYPES.JSXElement;
  children: JSXChild[];
  closingElement: JSXClosingElement | null;
  openingElement: JSXOpeningElement;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.JSXElement` | ✗ |  |
| `children` | `JSXChild[]` | ✗ |  |
| `closingElement` | `JSXClosingElement | null` | ✗ |  |
| `openingElement` | `JSXOpeningElement` | ✗ |  |


---