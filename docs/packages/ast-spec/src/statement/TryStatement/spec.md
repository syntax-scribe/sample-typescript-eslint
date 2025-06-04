[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

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