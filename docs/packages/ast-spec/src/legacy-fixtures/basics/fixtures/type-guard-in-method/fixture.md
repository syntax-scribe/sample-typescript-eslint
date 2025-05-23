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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/type-guard-in-method/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

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

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---