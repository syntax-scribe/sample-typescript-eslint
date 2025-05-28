[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `OptionalRangeAndLoc.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
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

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/OptionalRangeAndLoc.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Range` | `./Range` |
| `SourceLocation` | `./SourceLocation` |


---

## 🔧 Functions

> No functions found in this file.


---

## Type Aliases

### `OptionalRangeAndLoc<T>`

```ts
type OptionalRangeAndLoc<T> = {
  loc?: SourceLocation;
  range?: Range;
} & Pick<T, Exclude<keyof T, 'loc' | 'range'>>;
```


---