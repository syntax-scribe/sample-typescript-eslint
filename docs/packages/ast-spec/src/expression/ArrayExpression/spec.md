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
📂 **`packages/ast-spec/src/expression/ArrayExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `SpreadElement` | `../../element/SpreadElement/spec` |
| `Expression` | `../../unions/Expression` |


---

## Interfaces

### `ArrayExpression`

<details><summary>Interface Code</summary>

```ts
export interface ArrayExpression extends BaseNode {
  type: AST_NODE_TYPES.ArrayExpression;
  /**
   * an element will be `null` in the case of a sparse array: `[1, ,3]`
   */
  elements: (Expression | SpreadElement | null)[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ArrayExpression` | ✗ |  |
| `elements` | `(Expression | SpreadElement | null)[]` | ✗ |  |


---