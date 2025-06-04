[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isArray.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/utils/src/ts-utils/isArray.ts`**

## Functions

### `isArray(arg: unknown): arg is readonly unknown[]`

<details><summary>Code</summary>

```ts
export function isArray(arg: unknown): arg is readonly unknown[] {
  return Array.isArray(arg);
}
```
</details>

- **Parameters**:
  - `arg: unknown`
- **Return Type**: `arg is readonly unknown[]`
- **Calls**:
  - `Array.isArray`

---