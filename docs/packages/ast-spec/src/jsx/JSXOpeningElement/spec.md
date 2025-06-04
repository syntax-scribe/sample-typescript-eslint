[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 6 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

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