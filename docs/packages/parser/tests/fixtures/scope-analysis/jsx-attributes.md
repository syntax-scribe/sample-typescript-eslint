[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `jsx-attributes.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 2 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/jsx-attributes.tsx`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `text` | `"text"` | const | `'text'` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | *none* | <input> |
| `input` | element | type="search", size={30}, placeholder={text} | *none* |


---

## Functions

### `Foo(): any`

<details><summary>Code</summary>

```ts
export function Foo() {
  return (
    <div>
      <input type="search" size={30} placeholder={text} />
    </div>
  );
}
```
</details>

- **Return Type**: `any`

---