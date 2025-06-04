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
📂 **`packages/ast-spec/src/statement/SwitchStatement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `SwitchCase` | `../../special/SwitchCase/spec` |
| `Expression` | `../../unions/Expression` |


---

## Interfaces

### `SwitchStatement`

<details><summary>Interface Code</summary>

```ts
export interface SwitchStatement extends BaseNode {
  type: AST_NODE_TYPES.SwitchStatement;
  cases: SwitchCase[];
  discriminant: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.SwitchStatement` | ✗ |  |
| `cases` | `SwitchCase[]` | ✗ |  |
| `discriminant` | `Expression` | ✗ |  |


---