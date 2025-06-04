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
📂 **`packages/ast-spec/src/expression/ObjectExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `ObjectLiteralElement` | `../../unions/ObjectLiteralElement` |


---

## Interfaces

### `ObjectExpression`

<details><summary>Interface Code</summary>

```ts
export interface ObjectExpression extends BaseNode {
  type: AST_NODE_TYPES.ObjectExpression;
  properties: ObjectLiteralElement[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ObjectExpression` | ✗ |  |
| `properties` | `ObjectLiteralElement[]` | ✗ |  |


---