[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/function-with-type-parameters-with-constraint/fixture.ts`**

## Functions

### `a(b: X): X`

<details><summary>Code</summary>

```ts
function a<X extends {}>(b: X): X {
  return b;
}
```
</details>

- **Parameters**:
  - `b: X`
- **Return Type**: `X`

---