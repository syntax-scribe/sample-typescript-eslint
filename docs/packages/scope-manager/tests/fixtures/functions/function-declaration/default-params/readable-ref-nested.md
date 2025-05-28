[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `readable-ref-nested.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
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
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/functions/function-declaration/default-params/readable-ref-nested.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `a` | `any` | let/var | `*not shown*` | ✗ |


---

## Functions

### `foo(b: () => number): void`

<details><summary>Code</summary>

```ts
function foo(
  b = function () {
    return a;
  },
) {}
```
</details>

- **Parameters**:
  - `b: () => number`
- **Return Type**: `void`

---