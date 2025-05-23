[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `method.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 1
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/decorators/method.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `decorator(): void`

<details><summary>Code</summary>

```ts
function decorator() {}
```
</details>

- **Return Type**: `void`
### `Foo.foo(): void`

<details><summary>Code</summary>

```ts
@decorator
  foo() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  @decorator
  foo() {}
}
```
</details>

#### Methods

##### `foo(): void`

<details><summary>Code</summary>

```ts
@decorator
  foo() {}
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---