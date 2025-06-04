[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `readable-ref-nested-body-shadow.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/functions/function-expression/default-params/readable-ref-nested-body-shadow.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `a` | `any` | let/var | `*not shown*` | ✗ |
| `a` | `any` | let/var | `*not shown*` | ✗ |


---

## Functions

### `foo(b: () => void): void`

<details><summary>Code</summary>

```ts
function (
  b = function () {
    a;
  },
) {
  let a;
}
```
</details>

- **Parameters**:
  - `b: () => void`
- **Return Type**: `void`

---