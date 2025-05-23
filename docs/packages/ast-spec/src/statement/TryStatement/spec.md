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
📂 **`packages/ast-spec/src/statement/TryStatement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `CatchClause` | `../../special/CatchClause/spec` |
| `BlockStatement` | `../BlockStatement/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TryStatement`

<details><summary>Interface Code</summary>

```ts
export interface TryStatement extends BaseNode {
  type: AST_NODE_TYPES.TryStatement;
  block: BlockStatement;
  finalizer: BlockStatement | null;
  handler: CatchClause | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TryStatement` | ✗ |  |
| `block` | `BlockStatement` | ✗ |  |
| `finalizer` | `BlockStatement | null` | ✗ |  |
| `handler` | `CatchClause | null` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---