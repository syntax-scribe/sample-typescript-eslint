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
📂 **`packages/ast-spec/src/expression/JSXFragment/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `JSXClosingFragment` | `../../jsx/JSXClosingFragment/spec` |
| `JSXOpeningFragment` | `../../jsx/JSXOpeningFragment/spec` |
| `JSXChild` | `../../unions/JSXChild` |


---

## Interfaces

### `JSXFragment`

<details><summary>Interface Code</summary>

```ts
export interface JSXFragment extends BaseNode {
  type: AST_NODE_TYPES.JSXFragment;
  children: JSXChild[];
  closingFragment: JSXClosingFragment;
  openingFragment: JSXOpeningFragment;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.JSXFragment` | ✗ |  |
| `children` | `JSXChild[]` | ✗ |  |
| `closingFragment` | `JSXClosingFragment` | ✗ |  |
| `openingFragment` | `JSXOpeningFragment` | ✗ |  |


---