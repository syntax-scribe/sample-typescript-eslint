[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `LiteralBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/LiteralBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../ast-node-types` |
| `BaseNode` | `./BaseNode` |


---

## Interfaces

### `LiteralBase`

<details><summary>Interface Code</summary>

```ts
export interface LiteralBase extends BaseNode {
  type: AST_NODE_TYPES.Literal;
  raw: string;
  value: bigint | boolean | number | string | RegExp | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.Literal` | ✗ |  |
| `raw` | `string` | ✗ |  |
| `value` | `bigint | boolean | number | string | RegExp | null` | ✗ |  |


---