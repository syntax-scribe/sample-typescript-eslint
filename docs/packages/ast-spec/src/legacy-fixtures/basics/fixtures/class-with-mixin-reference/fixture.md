[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-with-mixin-reference/fixture.ts`**

## Functions

### `M(Base: T): void`

<details><summary>Code</summary>

```ts
function M<T extends Constructor<M>>(Base: T) {}
```
</details>

- **Parameters**:
  - `Base: T`
- **Return Type**: `void`

---