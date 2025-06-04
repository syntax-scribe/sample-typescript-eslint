[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/function-with-types-assignation/fixture.ts`**

## Functions

### `message(name: string, age: number, args: Array<string>): string`

<details><summary>Code</summary>

```ts
function message(
  name: string,
  age: number = 100,
  ...args: Array<string>
): string {
  return name;
}
```
</details>

- **Parameters**:
  - `name: string`
  - `age: number`
  - `args: Array<string>`
- **Return Type**: `string`

---