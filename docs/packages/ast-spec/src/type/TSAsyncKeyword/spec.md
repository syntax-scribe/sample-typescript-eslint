[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/type/TSAsyncKeyword/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |


---

## Interfaces

### `TSAsyncKeyword`

<details><summary>Interface Code</summary>

```ts
export interface TSAsyncKeyword extends BaseNode {
  type: AST_NODE_TYPES.TSAsyncKeyword;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSAsyncKeyword` | ✗ |  |


---