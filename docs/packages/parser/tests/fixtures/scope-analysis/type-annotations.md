[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `type-annotations.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 1
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/type-annotations.ts`**

## 📦 Imports

> No imports found in this file.


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

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `A`

```ts
type A = number;
```


---