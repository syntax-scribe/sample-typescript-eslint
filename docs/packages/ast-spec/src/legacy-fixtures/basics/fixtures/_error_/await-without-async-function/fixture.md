[⬅️ Back to Table of Contents](../../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 1 |
| ⚡ Async/Await Patterns | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Async/Await Patterns](#asyncawait-patterns)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/_error_/await-without-async-function/fixture.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `bar` | `void` | const | `await baz()` | ✗ |


---

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| await-expression | `foo` | baz() | *none* |


---

## Functions

### `foo(): any`

<details><summary>Code</summary>

```ts
function foo() {
  const bar = await baz();
  return bar.qux;
}
```
</details>

- **Return Type**: `any`
- **Calls**:
  - `baz`

---