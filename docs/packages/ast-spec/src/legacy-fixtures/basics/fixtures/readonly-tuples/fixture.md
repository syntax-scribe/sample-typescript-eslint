[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/readonly-tuples/fixture.ts`**

## Functions

### `foo(pair: readonly [string, string]): void`

<details><summary>Code</summary>

```ts
function foo(pair: readonly [string, string]) {
  console.log(pair[0]); // okay
  pair[1] = 'hello!'; // error
}
```
</details>

- **Parameters**:
  - `pair: readonly [string, string]`
- **Return Type**: `void`
- **Calls**:
  - `console.log`

---