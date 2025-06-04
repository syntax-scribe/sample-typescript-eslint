[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `inherited-scope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/functions/function-declaration/inherited-scope.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `parentScoped` | `1` | const | `1` | ✗ |


---

## Functions

### `foo(): void`

<details><summary>Code</summary>

```ts
function foo() {
  parentScoped + 1;
}
```
</details>

- **Return Type**: `void`

---