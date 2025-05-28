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
📂 **`packages/ast-spec/src/legacy-fixtures/parameter-decorators/fixtures/parameter-decorator-static-member/fixture.ts`**

## Functions

### `StaticGreeter.greet(name: string): string`

<details><summary>Code</summary>

```ts
static greet(@required name: string) {
    return 'Hello ' + name + '!';
  }
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `string`

---

## Classes

### `StaticGreeter`

<details><summary>Class Code</summary>

```ts
class StaticGreeter {
  static greet(@required name: string) {
    return 'Hello ' + name + '!';
  }
}
```
</details>

#### Methods

##### `greet(name: string): string`

<details><summary>Code</summary>

```ts
static greet(@required name: string) {
    return 'Hello ' + name + '!';
  }
```
</details>


---