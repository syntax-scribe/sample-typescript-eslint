[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 3 |
| ⚡ Async/Await Patterns | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Async/Await Patterns](#asyncawait-patterns)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/async-function-with-var-declaration/fixture.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `foo` | `string` | let/var | `'foo'` | ✗ |
| `bar` | `string` | let/var | `'bar'` | ✗ |
| `fooBar` | `"fooBar"` | let/var | `'fooBar'` | ✗ |


---

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| async-function | `test` | *none* | *none* |


---

## Functions

### `test(): Promise<void>`

<details><summary>Code</summary>

```ts
async function test() {
  var foo = 'foo';
  let bar = 'bar';
  const fooBar = 'fooBar';
}
```
</details>

- **Return Type**: `Promise<void>`

---