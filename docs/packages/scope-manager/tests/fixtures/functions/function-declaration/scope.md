[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `scope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/functions/function-declaration/scope.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `i` | `number` | let/var | `0` | ✗ |
| `j` | `number` | let/var | `20` | ✗ |
| `unresolved` | `any` | const | `j` | ✗ |


---

## Functions

### `foo(): void`

<details><summary>Code</summary>

```ts
function foo() {
  let i = 0;
  var j = 20;

  i;
}
```
</details>

- **Return Type**: `void`

---