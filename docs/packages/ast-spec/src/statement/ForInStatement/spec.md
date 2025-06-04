[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/statement/ForInStatement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |
| `ForInitialiser` | `../../unions/ForInitialiser` |
| `Statement` | `../../unions/Statement` |


---

## Interfaces

### `ForInStatement`

<details><summary>Interface Code</summary>

```ts
export interface ForInStatement extends BaseNode {
  type: AST_NODE_TYPES.ForInStatement;
  body: Statement;
  left: ForInitialiser;
  right: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ForInStatement` | ✗ |  |
| `body` | `Statement` | ✗ |  |
| `left` | `ForInitialiser` | ✗ |  |
| `right` | `Expression` | ✗ |  |


---