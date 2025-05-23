[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/FunctionExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `FunctionBase` | `../../base/FunctionBase` |
| `BlockStatement` | `../../statement/BlockStatement/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `FunctionExpression`

<details><summary>Interface Code</summary>

```ts
export interface FunctionExpression extends FunctionBase {
  type: AST_NODE_TYPES.FunctionExpression;
  body: BlockStatement;
  expression: false;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.FunctionExpression` | ✗ |  |
| `body` | `BlockStatement` | ✗ |  |
| `expression` | `false` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---