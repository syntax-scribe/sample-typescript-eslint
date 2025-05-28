[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `misc.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

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