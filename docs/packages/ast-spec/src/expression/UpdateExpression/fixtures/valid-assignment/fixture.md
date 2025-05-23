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
📂 **`packages/ast-spec/src/expression/UpdateExpression/fixtures/valid-assignment/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `F.m(): void`

<details><summary>Code</summary>

```ts
m() {
    this.#a++;
    this.m().a++;
    this[1] = 1;
    F++;
    // prettier-ignore
    (this.#a)++;
    (<number>this.#a)++;
    (this.#a satisfies number)++;
    (this.#a as number)++;
    this.#a!++;
  }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `this.m`
- **Internal Comments**:
```
// prettier-ignore (x3)
```


---

## Classes

### `F`

<details><summary>Class Code</summary>

```ts
class F {
  #a;

  m() {
    this.#a++;
    this.m().a++;
    this[1] = 1;
    F++;
    // prettier-ignore
    (this.#a)++;
    (<number>this.#a)++;
    (this.#a satisfies number)++;
    (this.#a as number)++;
    this.#a!++;
  }
}
```
</details>

#### Methods

##### `m(): void`

<details><summary>Code</summary>

```ts
m() {
    this.#a++;
    this.m().a++;
    this[1] = 1;
    F++;
    // prettier-ignore
    (this.#a)++;
    (<number>this.#a)++;
    (this.#a satisfies number)++;
    (this.#a as number)++;
    this.#a!++;
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