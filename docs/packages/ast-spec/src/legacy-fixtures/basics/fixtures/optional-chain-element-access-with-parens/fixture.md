[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/optional-chain-element-access-with-parens/fixture.ts`**

## Functions

### `processOptionalElementParens(one: any): void`

<details><summary>Code</summary>

```ts
function processOptionalElementParens(one?: any) {
  one?.[2];
  (one?.[2])[3];
  one[2]?.[3];
  (one[2]?.[3])[4];
  one[2]?.[3]?.[4];
  (one[2]?.[3]?.[4])[5];
}
```
</details>

- **Parameters**:
  - `one: any`
- **Return Type**: `void`

---