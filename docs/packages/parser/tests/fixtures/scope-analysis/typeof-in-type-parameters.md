[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `typeof-in-type-parameters.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/typeof-in-type-parameters.ts`**

## Functions

### `g(g: T): number`

<details><summary>Code</summary>

```ts
function g<T extends typeof g>(g: T): number {
  return 1;
}
```
</details>

- **Parameters**:
  - `g: T`
- **Return Type**: `number`

---