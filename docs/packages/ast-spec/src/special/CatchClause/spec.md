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
📂 **`packages/ast-spec/src/special/CatchClause/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `BlockStatement` | `../../statement/BlockStatement/spec` |
| `BindingName` | `../../unions/BindingName` |


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