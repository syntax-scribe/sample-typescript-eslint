[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/jsx/JSXMemberExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `JSXTagNameExpression` | `../../unions/JSXTagNameExpression` |
| `JSXIdentifier` | `../JSXIdentifier/spec` |


---

## Interfaces

### `JSXMemberExpression`

<details><summary>Interface Code</summary>

```ts
export interface JSXMemberExpression extends BaseNode {
  type: AST_NODE_TYPES.JSXMemberExpression;
  object: JSXTagNameExpression;
  property: JSXIdentifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.JSXMemberExpression` | ✗ |  |
| `object` | `JSXTagNameExpression` | ✗ |  |
| `property` | `JSXIdentifier` | ✗ |  |


---