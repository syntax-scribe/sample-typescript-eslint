[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `misc.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/test-utils/misc.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Variable` | `../../src` |
| `ImplicitLibVariable` | `../../src` |


---

## Functions

### `getRealVariables(variables: Variable[]): Variable[]`

<details><summary>Code</summary>

```ts
export function getRealVariables(variables: Variable[]): Variable[] {
  return variables.filter(v => !(v instanceof ImplicitLibVariable));
}
```
</details>

- **Parameters**:
  - `variables: Variable[]`
- **Return Type**: `Variable[]`
- **Calls**:
  - `variables.filter`

---