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
📂 **`packages/ast-spec/src/expression/BinaryExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `PrivateIdentifier` | `../../special/PrivateIdentifier/spec` |
| `Expression` | `../../unions/Expression` |
| `ValueOf` | `../../utils` |
| `BinaryOperatorToText` | `./BinaryOperatorToText` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `BinaryExpression`

<details><summary>Interface Code</summary>

```ts
export interface BinaryExpression extends BaseNode {
  type: AST_NODE_TYPES.BinaryExpression;
  left: Expression | PrivateIdentifier;
  operator: ValueOf<BinaryOperatorToText>;
  right: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.BinaryExpression` | ✗ |  |
| `left` | `Expression | PrivateIdentifier` | ✗ |  |
| `operator` | `ValueOf<BinaryOperatorToText>` | ✗ |  |
| `right` | `Expression` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---