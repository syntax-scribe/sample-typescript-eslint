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