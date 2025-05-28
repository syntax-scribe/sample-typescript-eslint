[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `type-predicate1.ts`

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
📂 **`packages/scope-manager/tests/fixtures/functions/function-expression/type-predicate1.ts`**

## Functions

### `foo(arg: any): arg is string`

<details><summary>Code</summary>

```ts
function (arg: any): arg is string {
  return typeof arg === 'string';
}
```
</details>

- **Parameters**:
  - `arg: any`
- **Return Type**: `arg is string`

---