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
📂 **`packages/ast-spec/src/type/TSLiteralType/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `UnaryExpression` | `../../expression/UnaryExpression/spec` |
| `UpdateExpression` | `../../expression/UpdateExpression/spec` |
| `LiteralExpression` | `../../unions/LiteralExpression` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSLiteralType`

<details><summary>Interface Code</summary>

```ts
export interface TSLiteralType extends BaseNode {
  type: AST_NODE_TYPES.TSLiteralType;
  literal: LiteralExpression | UnaryExpression | UpdateExpression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSLiteralType` | ✗ |  |
| `literal` | `LiteralExpression | UnaryExpression | UpdateExpression` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---