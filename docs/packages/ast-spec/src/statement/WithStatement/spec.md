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
📂 **`packages/ast-spec/src/statement/WithStatement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |
| `Statement` | `../../unions/Statement` |


---

## Interfaces

### `WithStatement`

<details><summary>Interface Code</summary>

```ts
export interface WithStatement extends BaseNode {
  type: AST_NODE_TYPES.WithStatement;
  body: Statement;
  object: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.WithStatement` | ✗ |  |
| `body` | `Statement` | ✗ |  |
| `object` | `Expression` | ✗ |  |


---