[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `UnaryExpressionBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/UnaryExpressionBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Expression` | `../unions/Expression` |
| `BaseNode` | `./BaseNode` |


---

## Interfaces

### `UnaryExpressionBase`

<details><summary>Interface Code</summary>

```ts
export interface UnaryExpressionBase extends BaseNode {
  argument: Expression;
  operator: string;
  prefix: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `argument` | `Expression` | ✗ |  |
| `operator` | `string` | ✗ |  |
| `prefix` | `boolean` | ✗ |  |


---