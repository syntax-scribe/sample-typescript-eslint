[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `assert.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/assert.ts`**

## Functions

### `assert(value: unknown, message: string): asserts value`

<details><summary>Code</summary>

```ts
export function assert(value: unknown, message?: string): asserts value {
  if (value == null) {
    throw new Error(message);
  }
}
```
</details>

- **Parameters**:
  - `value: unknown`
  - `message: string`
- **Return Type**: `asserts value`

---