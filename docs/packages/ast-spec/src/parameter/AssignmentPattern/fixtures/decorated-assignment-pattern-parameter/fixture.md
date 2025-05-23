[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

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
📂 **`packages/ast-spec/src/parameter/AssignmentPattern/fixtures/decorated-assignment-pattern-parameter/fixture.ts`**

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
### `A.foo(d: number): void`

<details><summary>Code</summary>

```ts
foo(@decorator d = 1) {}
```
</details>

- **Parameters**:
  - `d: number`
- **Return Type**: `void`

---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  foo(@decorator d = 1) {}
}
```
</details>

#### Methods

##### `foo(d: number): void`

<details><summary>Code</summary>

```ts
foo(@decorator d = 1) {}
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---