[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `enum.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📊 Variables & Constants | 1 |
| 🎯 Enums | 1 |


## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/enum.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `a` | `number` | const | `1` | ✗ |


---

## Enums

### `enum E`

<details><summary>Enum Code</summary>

```ts
enum E {
  A = a,
  B = a + 1,
  C = A + B,
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `A` | `a` |  |
| `B` | `a + 1` |  |
| `C` | `A + B` |  |


---