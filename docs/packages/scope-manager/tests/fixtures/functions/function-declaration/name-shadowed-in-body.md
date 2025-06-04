[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `name-shadowed-in-body.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 2 |

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