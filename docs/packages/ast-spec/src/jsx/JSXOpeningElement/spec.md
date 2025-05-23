[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/jsx/JSXOpeningElement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TSTypeParameterInstantiation` | `../../special/TSTypeParameterInstantiation/spec` |
| `JSXTagNameExpression` | `../../unions/JSXTagNameExpression` |
| `JSXAttribute` | `../JSXAttribute/spec` |
| `JSXSpreadAttribute` | `../JSXSpreadAttribute/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `JSXOpeningElement`

<details><summary>Interface Code</summary>

```ts
export interface JSXOpeningElement extends BaseNode {
  type: AST_NODE_TYPES.JSXOpeningElement;
  attributes: (JSXAttribute | JSXSpreadAttribute)[];
  name: JSXTagNameExpression;
  selfClosing: boolean;
  typeArguments: TSTypeParameterInstantiation | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.JSXOpeningElement` | ✗ |  |
| `attributes` | `(JSXAttribute | JSXSpreadAttribute)[]` | ✗ |  |
| `name` | `JSXTagNameExpression` | ✗ |  |
| `selfClosing` | `boolean` | ✗ |  |
| `typeArguments` | `TSTypeParameterInstantiation | undefined` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---