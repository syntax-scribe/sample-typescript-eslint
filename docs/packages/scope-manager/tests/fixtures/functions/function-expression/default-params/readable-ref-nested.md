[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `readable-ref-nested.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/functions/function-expression/default-params/readable-ref-nested.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `a` | `any` | let/var | `*not shown*` | ✗ |


---

## Functions

### `foo(b: () => number): void`

<details><summary>Code</summary>

```ts
function (
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