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
📂 **`packages/ast-spec/src/statement/ForStatement/spec.ts`**

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

### `ForStatement`

<details><summary>Interface Code</summary>

```ts
export interface ForStatement extends BaseNode {
  type: AST_NODE_TYPES.ForStatement;
  body: Statement;
  init: Expression | ForInitialiser | null;
  test: Expression | null;
  update: Expression | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ForStatement` | ✗ |  |
| `body` | `Statement` | ✗ |  |
| `init` | `Expression | ForInitialiser | null` | ✗ |  |
| `test` | `Expression | null` | ✗ |  |
| `update` | `Expression | null` | ✗ |  |


---