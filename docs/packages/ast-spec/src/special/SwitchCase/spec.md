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
📂 **`packages/ast-spec/src/special/SwitchCase/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |
| `Statement` | `../../unions/Statement` |


---

## Interfaces

### `SwitchCase`

<details><summary>Interface Code</summary>

```ts
export interface SwitchCase extends BaseNode {
  type: AST_NODE_TYPES.SwitchCase;
  consequent: Statement[];
  test: Expression | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.SwitchCase` | ✗ |  |
| `consequent` | `Statement[]` | ✗ |  |
| `test` | `Expression | null` | ✗ |  |


---