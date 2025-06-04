[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/nullish-coalescing/fixture.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `len` | `string` | let/var | `s ?? ''` | ✗ |


---

## Functions

### `processNullishCoalesce(s: string): void`

<details><summary>Code</summary>

```ts
function processNullishCoalesce(s?: string) {
  let len = s ?? '';
}
```
</details>

- **Parameters**:
  - `s: string`
- **Return Type**: `void`

---