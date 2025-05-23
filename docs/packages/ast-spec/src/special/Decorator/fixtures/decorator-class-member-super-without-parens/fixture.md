[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 2
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/special/Decorator/fixtures/decorator-class-member-super-without-parens/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `D.m(): void`

<details><summary>Code</summary>

```ts
m() {
    class C {
      @(super.decorate) // note the lack of parentheses
      method2() {}
    }
  }
```
</details>

- **Return Type**: `void`
### `C.method2(): void`

<details><summary>Code</summary>

```ts
@(super.decorate) // note the lack of parentheses
      method2() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `D`

<details><summary>Class Code</summary>

```ts
class D extends DecoratorProvider {
  m() {
    class C {
      @(super.decorate) // note the lack of parentheses
      method2() {}
    }
  }
}
```
</details>

#### Methods

##### `m(): void`

<details><summary>Code</summary>

```ts
m() {
    class C {
      @(super.decorate) // note the lack of parentheses
      method2() {}
    }
  }
```
</details>

### `C`

<details><summary>Class Code</summary>

```ts
class C {
      @(super.decorate) // note the lack of parentheses
      method2() {}
    }
```
</details>

#### Methods

##### `method2(): void`

<details><summary>Code</summary>

```ts
@(super.decorate) // note the lack of parentheses
      method2() {}
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---