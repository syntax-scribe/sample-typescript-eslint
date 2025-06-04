[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| ⚡ Async/Await Patterns | 1 |

## 📚 Table of Contents

- [Async/Await Patterns](#asyncawait-patterns)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/function-with-await/fixture.ts`**

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| async-function | `hope` | future | *none* |


---

## Functions

### `hope(future: any): Promise<void>`

<details><summary>Code</summary>

```ts
async function hope(future) {
  await future;
}
```
</details>

- **Parameters**:
  - `future: any`
- **Return Type**: `Promise<void>`

---