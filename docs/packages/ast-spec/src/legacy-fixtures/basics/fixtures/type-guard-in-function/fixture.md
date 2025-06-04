[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/type-guard-in-function/fixture.ts`**

## Functions

### `isString(x: any): x is string`

<details><summary>Code</summary>

```ts
function isString(x: any): x is string {
  return typeof x === 'string';
}
```
</details>

- **Parameters**:
  - `x: any`
- **Return Type**: `x is string`

---