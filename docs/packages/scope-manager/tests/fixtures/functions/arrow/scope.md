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
📂 **`packages/scope-manager/tests/fixtures/functions/arrow/scope.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `i` | `number` | let/var | `0` | ✗ |
| `j` | `number` | let/var | `20` | ✗ |
| `unresolved` | `any` | const | `j` | ✗ |


---

## Functions

### `arrow(): void`

<details><summary>Code</summary>

```ts
() => {
  let i = 0;
  var j = 20;

  i;
}
```
</details>

- **Return Type**: `void`

---