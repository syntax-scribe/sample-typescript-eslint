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
📂 **`packages/ast-spec/src/special/Decorator/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `LeftHandSideExpression` | `../../unions/LeftHandSideExpression` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `Decorator`

<details><summary>Interface Code</summary>

```ts
export interface Decorator extends BaseNode {
  type: AST_NODE_TYPES.Decorator;
  expression: LeftHandSideExpression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.Decorator` | ✗ |  |
| `expression` | `LeftHandSideExpression` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---