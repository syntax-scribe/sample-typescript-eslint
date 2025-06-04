[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/readonly-arrays/fixture.ts`**

## Functions

### `foo(arr: ReadonlyArray<string>): void`

<details><summary>Code</summary>

```ts
function foo(arr: ReadonlyArray<string>) {
  arr.slice(); // okay
  arr.push('hello!'); // error!
}
```
</details>

- **Parameters**:
  - `arr: ReadonlyArray<string>`
- **Return Type**: `void`
- **Calls**:
  - `arr.slice`
  - `arr.push`

---