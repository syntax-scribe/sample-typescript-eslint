[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `type-arguments1.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 2 |
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

- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/instantiation-expressions/type-arguments1.ts`**

## 🔧 Functions

> No functions found in this file.


---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo<T> {
  value: T;
}
```
</details>

### `Bar`

<details><summary>Class Code</summary>

```ts
class Bar<T> {
  foo = Foo<T>;
}
```
</details>


---