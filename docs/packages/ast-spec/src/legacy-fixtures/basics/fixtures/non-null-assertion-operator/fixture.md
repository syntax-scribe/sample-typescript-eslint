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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/non-null-assertion-operator/fixture.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `s` | `any` | let/var | `e!.name` | ✗ |


---

## Functions

### `processEntity(e: Entity): void`

<details><summary>Code</summary>

```ts
function processEntity(e?: Entity) {
  validateEntity(e);
  let s = e!.name;
}
```
</details>

- **Parameters**:
  - `e: Entity`
- **Return Type**: `void`
- **Calls**:
  - `validateEntity`

---