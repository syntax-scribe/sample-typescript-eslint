[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Utility.vue`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 1 |
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
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/integration-tests/fixtures/vue-sfc/Utility.vue`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `list` | `Array<string>` | const | `[]` | ✗ |
| `a` | `string[]` | const | `this.a as Array<string>` | ✗ |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

### `Utility`

<details><summary>Class Code</summary>

```ts
export default class Utility {
  get a() {
    const list: Array<string> = [];
    return list;
  }

  get b() {
    const a = this.a as Array<string>;
    return a;
  }
}
```
</details>


---