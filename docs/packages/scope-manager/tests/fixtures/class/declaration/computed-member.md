[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `computed-member.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
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
- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/class/declaration/computed-member.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `outer1` | `"a"` | const | `'a'` | ✗ |
| `outer2` | `"b"` | const | `'b'` | ✗ |


---

## Functions

### `A.[outer2](): void`

<details><summary>Code</summary>

```ts
[outer2]() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  [outer1] = 1;
  [outer2]() {}
}
```
</details>

#### Methods

##### `[outer2](): void`

<details><summary>Code</summary>

```ts
[outer2]() {}
```
</details>


---