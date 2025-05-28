[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `method-overload.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
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
📂 **`packages/parser/tests/fixtures/scope-analysis/method-overload.ts`**

## Functions

### `A.f(): void`

<details><summary>Code</summary>

```ts
f(): void;
```
</details>

- **Return Type**: `void`
### `A.f(a: typeof s): void`

<details><summary>Code</summary>

```ts
f(a: typeof s): void;
```
</details>

- **Parameters**:
  - `a: typeof s`
- **Return Type**: `void`
### `A.f(a: any): void`

<details><summary>Code</summary>

```ts
f(a?: any): void {
    // do something.
  }
```
</details>

- **Parameters**:
  - `a: any`
- **Return Type**: `void`

---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  f(): void;
  f(a: typeof s): void;
  f(a?: any): void {
    // do something.
  }
}
```
</details>

#### Methods

##### `f(): void`

<details><summary>Code</summary>

```ts
f(): void;
```
</details>

##### `f(a: typeof s): void`

<details><summary>Code</summary>

```ts
f(a: typeof s): void;
```
</details>

##### `f(a: any): void`

<details><summary>Code</summary>

```ts
f(a?: any): void {
    // do something.
  }
```
</details>


---