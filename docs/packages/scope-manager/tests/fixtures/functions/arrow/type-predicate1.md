[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `type-predicate1.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/functions/arrow/type-predicate1.ts`**

## Functions

### `foo(arg: any): arg is string`

<details><summary>Code</summary>

```ts
(arg: any): arg is string => {
  return typeof arg === 'string';
}
```
</details>

- **Parameters**:
  - `arg: any`
- **Return Type**: `arg is string`

---