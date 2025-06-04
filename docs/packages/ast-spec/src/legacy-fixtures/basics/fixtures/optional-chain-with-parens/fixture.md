[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/optional-chain-with-parens/fixture.ts`**

## Functions

### `processOptionalParens(one: any): void`

<details><summary>Code</summary>

```ts
function processOptionalParens(one?: any) {
  one?.two;
  (one?.two).three;
  one.two?.three;
  (one.two?.three).four;
  one.two?.three?.four;
  (one.two?.three?.four).five;
}
```
</details>

- **Parameters**:
  - `one: any`
- **Return Type**: `void`

---