[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 1 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 2 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-with-optional-properties/fixture.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `computed` | `"buzz"` | const | `'buzz'` | ✗ |
| `computed2` | `"bazz"` | const | `'bazz'` | ✗ |


---


---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  foo?;
  bar?: string;
  private baz?: string;
  [computed]?;
  ['literal']?;
  [1]?;
  [computed2]?: string;
  ['literal2']?: string;
  [2]?: string;
}
```
</details>


---