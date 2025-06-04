[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/jsx/JSXClosingElement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `JSXTagNameExpression` | `../../unions/JSXTagNameExpression` |


---

## Interfaces

### `JSXClosingElement`

<details><summary>Interface Code</summary>

```ts
export interface JSXClosingElement extends BaseNode {
  type: AST_NODE_TYPES.JSXClosingElement;
  name: JSXTagNameExpression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.JSXClosingElement` | ✗ |  |
| `name` | `JSXTagNameExpression` | ✗ |  |


---