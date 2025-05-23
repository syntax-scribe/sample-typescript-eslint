[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 1
- **Type Aliases**: 0

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

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---