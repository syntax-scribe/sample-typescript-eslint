[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `interface-type.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/interface-type.ts`**

## 🔧 Functions

> No functions found in this file.


---

## Interfaces

### `C<T = any>`

<details><summary>Interface Code</summary>

```ts
interface C<T = any> {}
```
</details>

### `R<T extends C>`

<details><summary>Interface Code</summary>

```ts
interface R<T extends C> {
  foo: C;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `foo` | `C` | ✗ |  |


---