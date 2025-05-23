[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 1
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/type-assertion-in-method/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `AssertsFoo.isBar(): asserts this`

<details><summary>Code</summary>

```ts
isBar(): asserts this {
    return;
  }
```
</details>

- **Return Type**: `asserts this`

---

## Classes

### `AssertsFoo`

<details><summary>Class Code</summary>

```ts
class AssertsFoo {
  isBar(): asserts this {
    return;
  }
  isBaz = (): asserts this => {
    return;
  };
}
```
</details>

#### Methods

##### `isBar(): asserts this`

<details><summary>Code</summary>

```ts
isBar(): asserts this {
    return;
  }
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---