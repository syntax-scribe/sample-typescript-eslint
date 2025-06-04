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
📂 **`packages/ast-spec/src/special/ImportAttribute/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `Literal` | `../../unions/Literal` |


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