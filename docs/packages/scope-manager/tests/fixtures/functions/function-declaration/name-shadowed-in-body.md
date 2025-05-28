[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `name-shadowed-in-body.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 2 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/functions/function-declaration/name-shadowed-in-body.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `Foo` | `1` | const | `1` | ✗ |
| `usage` | `typeof Foo` | const | `Foo` | ✗ |


---

## Functions

### `Foo(): void`

<details><summary>Code</summary>

```ts
function Foo() {
  const Foo = 1;
}
```
</details>

- **Return Type**: `void`

---