[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/UnaryExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `UnaryExpressionBase` | `../../base/UnaryExpressionBase` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `UnaryExpression`

<details><summary>Interface Code</summary>

```ts
export interface UnaryExpression extends UnaryExpressionBase {
  type: AST_NODE_TYPES.UnaryExpression;
  operator: '!' | '+' | '-' | 'delete' | 'typeof' | 'void' | '~';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.UnaryExpression` | ✗ |  |
| `operator` | `'!' | '+' | '-' | 'delete' | 'typeof' | 'void' | '~'` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---