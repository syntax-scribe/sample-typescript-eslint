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
📂 **`packages/ast-spec/src/special/ImportAttribute/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `Literal` | `../../unions/Literal` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ImportAttribute`

<details><summary>Interface Code</summary>

```ts
export interface ImportAttribute extends BaseNode {
  type: AST_NODE_TYPES.ImportAttribute;
  key: Identifier | Literal;
  value: Literal;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ImportAttribute` | ✗ |  |
| `key` | `Identifier | Literal` | ✗ |  |
| `value` | `Literal` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---