[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
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

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/special/Decorator/fixtures/decorator-class-member-super-without-parens/fixture.ts`**

## Functions

### `D.m(): void`

<details><summary>Code</summary>

```ts
m() {
    class C {
      @(super.decorate) // note the lack of parentheses
      method2() {}
    }
  }
```
</details>

- **Return Type**: `void`
### `C.method2(): void`

<details><summary>Code</summary>

```ts
@(super.decorate) // note the lack of parentheses
      method2() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `D`

<details><summary>Class Code</summary>

```ts
class D extends DecoratorProvider {
  m() {
    class C {
      @(super.decorate) // note the lack of parentheses
      method2() {}
    }
  }
}
```
</details>

#### Methods

##### `m(): void`

<details><summary>Code</summary>

```ts
m() {
    class C {
      @(super.decorate) // note the lack of parentheses
      method2() {}
    }
  }
```
</details>

### `C`

<details><summary>Class Code</summary>

```ts
class C {
      @(super.decorate) // note the lack of parentheses
      method2() {}
    }
```
</details>

#### Methods

##### `method2(): void`

<details><summary>Code</summary>

```ts
@(super.decorate) // note the lack of parentheses
      method2() {}
```
</details>


---