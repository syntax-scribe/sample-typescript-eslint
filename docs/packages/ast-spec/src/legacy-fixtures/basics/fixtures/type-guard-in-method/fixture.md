[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |
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
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/type-guard-in-method/fixture.ts`**

## Functions

### `Foo.isBar(): this is string`

<details><summary>Code</summary>

```ts
isBar(): this is string {
    return this instanceof Foo;
  }
```
</details>

- **Return Type**: `this is string`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  isBar(): this is string {
    return this instanceof Foo;
  }
  isBaz = (): this is string => {
    return this instanceof Foo;
  };
}
```
</details>

#### Methods

##### `isBar(): this is string`

<details><summary>Code</summary>

```ts
isBar(): this is string {
    return this instanceof Foo;
  }
```
</details>


---