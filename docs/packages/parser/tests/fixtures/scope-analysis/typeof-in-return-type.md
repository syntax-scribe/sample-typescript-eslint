[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `typeof-in-return-type.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/typeof-in-return-type.ts`**

## Functions

### `f(a: number): typeof a`

<details><summary>Code</summary>

```ts
function f(a: number): typeof a {
  // this `a` is the parameter `a`.
  return 1;
}
```
</details>

- **Parameters**:
  - `a: number`
- **Return Type**: `typeof a`
- **Internal Comments**:
```
// this `a` is the parameter `a`.
```


---