[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/optional-chain-element-access/fixture.ts`**

## Functions

### `processOptionalElement(one: any): void`

<details><summary>Code</summary>

```ts
function processOptionalElement(one?: any) {
  one?.[2];
  one?.[2][3];
  one[2]?.[3];
  one[2]?.[3];
  one[2]?.[3][4];
  one[2]?.[3]?.[4];
}
```
</details>

- **Parameters**:
  - `one: any`
- **Return Type**: `void`

---