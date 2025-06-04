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
📂 **`packages/ast-spec/src/statement/ForOfStatement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |
| `ForOfInitialiser` | `../../unions/ForOfInitialiser` |
| `Statement` | `../../unions/Statement` |


---

## Interfaces

### `ForOfStatement`

<details><summary>Interface Code</summary>

```ts
export interface ForOfStatement extends BaseNode {
  type: AST_NODE_TYPES.ForOfStatement;
  await: boolean;
  body: Statement;
  left: ForOfInitialiser;
  right: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ForOfStatement` | ✗ |  |
| `await` | `boolean` | ✗ |  |
| `body` | `Statement` | ✗ |  |
| `left` | `ForOfInitialiser` | ✗ |  |
| `right` | `Expression` | ✗ |  |


---