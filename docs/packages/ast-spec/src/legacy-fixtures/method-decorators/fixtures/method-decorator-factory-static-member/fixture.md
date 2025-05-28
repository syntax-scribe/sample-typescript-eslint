[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 1 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Decorators](#decorators)
- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/method-decorators/fixtures/method-decorator-factory-static-member/fixture.ts`**

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@Foo` | `C.staticMethod` | method | false |


---

## Functions

### `C.staticMethod(): void`

<details><summary>Code</summary>

```ts
@Foo(false)
  static staticMethod() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `C`

<details><summary>Class Code</summary>

```ts
class C {
  @Foo(false)
  static staticMethod() {}
}
```
</details>

#### Methods

##### `staticMethod(): void`

<details><summary>Code</summary>

```ts
@Foo(false)
  static staticMethod() {}
```
</details>


---