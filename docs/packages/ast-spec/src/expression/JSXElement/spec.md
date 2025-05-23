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

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---