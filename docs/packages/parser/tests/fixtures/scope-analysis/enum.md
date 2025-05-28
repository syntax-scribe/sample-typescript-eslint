[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `enum.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
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

## 🔧 Functions

> No functions found in this file.


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