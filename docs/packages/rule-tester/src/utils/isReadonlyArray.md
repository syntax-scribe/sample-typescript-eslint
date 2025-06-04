[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isReadonlyArray.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/isReadonlyArray.ts`**

## Functions

### `isReadonlyArray(arg: unknown): arg is readonly unknown[]`

<details><summary>Code</summary>

```ts
export function isReadonlyArray(arg: unknown): arg is readonly unknown[] {
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