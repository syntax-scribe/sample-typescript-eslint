[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `typeof-in-type-parameters.ts`

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
📂 **`packages/parser/tests/fixtures/scope-analysis/typeof-in-type-parameters.ts`**

## Functions

### `g(g: T): number`

<details><summary>Code</summary>

```ts
function g<T extends typeof g>(g: T): number {
  return 1;
}
```
</details>

- **Parameters**:
  - `g: T`
- **Return Type**: `number`

---