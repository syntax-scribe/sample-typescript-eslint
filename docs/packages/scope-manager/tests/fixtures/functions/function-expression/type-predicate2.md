[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `type-predicate2.ts`

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
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/functions/function-expression/type-predicate2.ts`**

## Functions

### `foo(arg: any): arg is T`

<details><summary>Code</summary>

```ts
function (arg: any): arg is T {
  return typeof arg === 'string';
}
```
</details>

- **Parameters**:
  - `arg: any`
- **Return Type**: `arg is T`

---

## Type Aliases

### `T`

```ts
type T = string;
```


---