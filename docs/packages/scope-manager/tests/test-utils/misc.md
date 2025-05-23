[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `misc.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---