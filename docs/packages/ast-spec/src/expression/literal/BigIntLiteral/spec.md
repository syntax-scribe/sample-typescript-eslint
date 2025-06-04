[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 1 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/literal/BigIntLiteral/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `LiteralBase` | `../../../base/LiteralBase` |


---

## Interfaces

### `BigIntLiteral`

<details><summary>Interface Code</summary>

```ts
export interface BigIntLiteral extends LiteralBase {
  bigint: string;
  value: bigint | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `bigint` | `string` | ✗ |  |
| `value` | `bigint | null` | ✗ |  |


---