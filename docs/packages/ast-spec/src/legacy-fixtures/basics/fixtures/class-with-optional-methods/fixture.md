[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 1
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-with-optional-methods/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `Foo.foo(): any`

<details><summary>Code</summary>

```ts
foo?();
```
</details>

- **Return Type**: `any`
### `Foo.bar(): string`

<details><summary>Code</summary>

```ts
bar?(): string;
```
</details>

- **Return Type**: `string`
### `Foo.baz(): string`

<details><summary>Code</summary>

```ts
private baz?(): string;
```
</details>

- **Return Type**: `string`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  foo?();
  bar?(): string;
  private baz?(): string;
}
```
</details>

#### Methods

##### `foo(): any`

<details><summary>Code</summary>

```ts
foo?();
```
</details>

##### `bar(): string`

<details><summary>Code</summary>

```ts
bar?(): string;
```
</details>

##### `baz(): string`

<details><summary>Code</summary>

```ts
private baz?(): string;
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---