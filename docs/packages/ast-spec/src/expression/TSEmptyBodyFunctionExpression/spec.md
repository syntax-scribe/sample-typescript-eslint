[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/TSEmptyBodyFunctionExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `FunctionBase` | `../../base/FunctionBase` |


---

## Interfaces

### `TSEmptyBodyFunctionExpression`

<details><summary>Interface Code</summary>

```ts
export interface TSEmptyBodyFunctionExpression extends FunctionBase {
  type: AST_NODE_TYPES.TSEmptyBodyFunctionExpression;
  body: null;
  id: null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSEmptyBodyFunctionExpression` | ✗ |  |
| `body` | `null` | ✗ |  |
| `id` | `null` | ✗ |  |


---