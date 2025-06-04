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
📂 **`packages/ast-spec/src/statement/IfStatement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |
| `Statement` | `../../unions/Statement` |


---

## Interfaces

### `IfStatement`

<details><summary>Interface Code</summary>

```ts
export interface IfStatement extends BaseNode {
  type: AST_NODE_TYPES.IfStatement;
  alternate: Statement | null;
  consequent: Statement;
  test: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.IfStatement` | ✗ |  |
| `alternate` | `Statement | null` | ✗ |  |
| `consequent` | `Statement` | ✗ |  |
| `test` | `Expression` | ✗ |  |


---