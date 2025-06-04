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
📂 **`packages/ast-spec/src/statement/LabeledStatement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `Statement` | `../../unions/Statement` |


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