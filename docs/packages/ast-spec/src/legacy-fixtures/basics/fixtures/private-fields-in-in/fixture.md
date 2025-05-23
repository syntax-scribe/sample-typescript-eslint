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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/private-fields-in-in/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `Foo.method(arg: any): boolean`

<details><summary>Code</summary>

```ts
method(arg) {
    return #prop1 in arg;
  }
```
</details>

- **Parameters**:
  - `arg: any`
- **Return Type**: `boolean`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  #prop1;
  method(arg) {
    return #prop1 in arg;
  }
}
```
</details>

#### Methods

##### `method(arg: any): boolean`

<details><summary>Code</summary>

```ts
method(arg) {
    return #prop1 in arg;
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