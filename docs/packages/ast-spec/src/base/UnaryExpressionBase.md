[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `UnaryExpressionBase.ts`

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
📂 **`packages/ast-spec/src/base/UnaryExpressionBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Expression` | `../unions/Expression` |
| `BaseNode` | `./BaseNode` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `UnaryExpressionBase`

<details><summary>Interface Code</summary>

```ts
export interface UnaryExpressionBase extends BaseNode {
  argument: Expression;
  operator: string;
  prefix: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `argument` | `Expression` | ✗ |  |
| `operator` | `string` | ✗ |  |
| `prefix` | `boolean` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---