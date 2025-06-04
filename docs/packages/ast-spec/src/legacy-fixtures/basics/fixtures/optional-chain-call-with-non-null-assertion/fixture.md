[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/optional-chain-call-with-non-null-assertion/fixture.ts`**

## Functions

### `processOptional(one: any): void`

<details><summary>Code</summary>

```ts
function processOptional(one?: any) {
  one?.two!();
  one?.two!.three();
  one?.two!();
  one?.two!.three();
  one?.two!();
  one?.two!.three();
}
```
</details>

- **Parameters**:
  - `one: any`
- **Return Type**: `void`
- **Calls**:
  - `complex_call_113`
  - `one?.two!.three`
  - `complex_call_149`
  - `complex_call_185`

---