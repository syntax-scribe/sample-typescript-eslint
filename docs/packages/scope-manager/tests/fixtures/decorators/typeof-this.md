[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `typeof-this.ts`

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
📂 **`packages/scope-manager/tests/fixtures/decorators/typeof-this.ts`**

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
### `Foo.bar(baz: typeof this): void`

<details><summary>Code</summary>

```ts
bar(baz: typeof this) {}
```
</details>

- **Parameters**:
  - `baz: typeof this`
- **Return Type**: `void`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
@decorator
class Foo {
  bar(baz: typeof this) {}
}
```
</details>

#### Methods

##### `bar(baz: typeof this): void`

<details><summary>Code</summary>

```ts
bar(baz: typeof this) {}
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---