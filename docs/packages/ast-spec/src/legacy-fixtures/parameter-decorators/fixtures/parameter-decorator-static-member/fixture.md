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
📂 **`packages/ast-spec/src/legacy-fixtures/parameter-decorators/fixtures/parameter-decorator-static-member/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `StaticGreeter.greet(name: string): string`

<details><summary>Code</summary>

```ts
static greet(@required name: string) {
    return 'Hello ' + name + '!';
  }
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `string`

---

## Classes

### `StaticGreeter`

<details><summary>Class Code</summary>

```ts
class StaticGreeter {
  static greet(@required name: string) {
    return 'Hello ' + name + '!';
  }
}
```
</details>

#### Methods

##### `greet(name: string): string`

<details><summary>Code</summary>

```ts
static greet(@required name: string) {
    return 'Hello ' + name + '!';
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