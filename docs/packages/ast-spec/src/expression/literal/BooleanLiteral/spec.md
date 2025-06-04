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
📂 **`packages/ast-spec/src/expression/literal/BooleanLiteral/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `LiteralBase` | `../../../base/LiteralBase` |


---

## Interfaces

### `BooleanLiteral`

<details><summary>Interface Code</summary>

```ts
export interface BooleanLiteral extends LiteralBase {
  raw: 'false' | 'true';
  value: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `raw` | `'false' | 'true'` | ✗ |  |
| `value` | `boolean` | ✗ |  |


---