[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `type-annotations.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Classes](#classes)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/type-annotations.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `a` | `{ b: A }` | let/var | `*not shown*` | ✗ |


---

## Functions

### `C.f(a: { b: A }): { b: A }`

<details><summary>Code</summary>

```ts
f(a: { b: A }): { b: A } {
    return { b: 1 };
  }
```
</details>

- **Parameters**:
  - `a: { b: A }`
- **Return Type**: `{ b: A }`

---

## Classes

### `C`

<details><summary>Class Code</summary>

```ts
class C {
  f(a: { b: A }): { b: A } {
    return { b: 1 };
  }
}
```
</details>

#### Methods

##### `f(a: { b: A }): { b: A }`

<details><summary>Code</summary>

```ts
f(a: { b: A }): { b: A } {
    return { b: 1 };
  }
```
</details>


---

## Type Aliases

### `A`

```ts
type A = number;
```


---