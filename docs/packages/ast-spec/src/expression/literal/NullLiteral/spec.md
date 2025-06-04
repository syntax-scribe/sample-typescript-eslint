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
📂 **`packages/ast-spec/src/expression/literal/NullLiteral/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `LiteralBase` | `../../../base/LiteralBase` |


---

## Interfaces

### `NullLiteral`

<details><summary>Interface Code</summary>

```ts
export interface NullLiteral extends LiteralBase {
  raw: 'null';
  value: null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `raw` | `'null'` | ✗ |  |
| `value` | `null` | ✗ |  |


---