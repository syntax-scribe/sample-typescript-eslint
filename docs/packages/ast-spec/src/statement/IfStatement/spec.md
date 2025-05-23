[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/statement/IfStatement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |
| `Statement` | `../../unions/Statement` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `IfStatement`

<details><summary>Interface Code</summary>

```ts
export interface IfStatement extends BaseNode {
  type: AST_NODE_TYPES.IfStatement;
  alternate: Statement | null;
  consequent: Statement;
  test: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.IfStatement` | ✗ |  |
| `alternate` | `Statement | null` | ✗ |  |
| `consequent` | `Statement` | ✗ |  |
| `test` | `Expression` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---