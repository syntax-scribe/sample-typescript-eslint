[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Utility.vue`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📊 Variables & Constants | 2 |

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