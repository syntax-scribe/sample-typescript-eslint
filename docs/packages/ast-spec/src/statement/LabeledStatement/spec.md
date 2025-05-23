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
📂 **`packages/ast-spec/src/statement/LabeledStatement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `Statement` | `../../unions/Statement` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `LabeledStatement`

<details><summary>Interface Code</summary>

```ts
export interface LabeledStatement extends BaseNode {
  type: AST_NODE_TYPES.LabeledStatement;
  body: Statement;
  label: Identifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.LabeledStatement` | ✗ |  |
| `body` | `Statement` | ✗ |  |
| `label` | `Identifier` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---