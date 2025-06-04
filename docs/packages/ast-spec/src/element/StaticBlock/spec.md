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
📂 **`packages/ast-spec/src/element/StaticBlock/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Statement` | `../../unions/Statement` |


---

## Interfaces

### `StaticBlock`

<details><summary>Interface Code</summary>

```ts
export interface StaticBlock extends BaseNode {
  type: AST_NODE_TYPES.StaticBlock;
  body: Statement[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.StaticBlock` | ✗ |  |
| `body` | `Statement[]` | ✗ |  |


---