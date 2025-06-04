[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/FunctionExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `FunctionBase` | `../../base/FunctionBase` |
| `BlockStatement` | `../../statement/BlockStatement/spec` |


---

## Interfaces

### `FunctionExpression`

<details><summary>Interface Code</summary>

```ts
export interface FunctionExpression extends FunctionBase {
  type: AST_NODE_TYPES.FunctionExpression;
  body: BlockStatement;
  expression: false;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.FunctionExpression` | ✗ |  |
| `body` | `BlockStatement` | ✗ |  |
| `expression` | `false` | ✗ |  |


---