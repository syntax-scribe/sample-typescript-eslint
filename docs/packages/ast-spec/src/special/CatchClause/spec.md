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
📂 **`packages/ast-spec/src/special/CatchClause/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `BlockStatement` | `../../statement/BlockStatement/spec` |
| `BindingName` | `../../unions/BindingName` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `CatchClause`

<details><summary>Interface Code</summary>

```ts
export interface CatchClause extends BaseNode {
  type: AST_NODE_TYPES.CatchClause;
  body: BlockStatement;
  param: BindingName | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.CatchClause` | ✗ |  |
| `body` | `BlockStatement` | ✗ |  |
| `param` | `BindingName | null` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---