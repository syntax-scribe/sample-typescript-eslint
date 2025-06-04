[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/statement/BlockStatement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Statement` | `../../unions/Statement` |


---

## Interfaces

### `BlockStatement`

<details><summary>Interface Code</summary>

```ts
export interface BlockStatement extends BaseNode {
  type: AST_NODE_TYPES.BlockStatement;
  body: Statement[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.BlockStatement` | ✗ |  |
| `body` | `Statement[]` | ✗ |  |


---