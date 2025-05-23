[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `nullThrows.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/utils/src/eslint-utils/nullThrows.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `MissingToken(token: string, thing: string): string`

<details><summary>Code</summary>

```ts
(token: string, thing: string) =>
    `Expected to find a ${token} for the ${thing}.`
```
</details>

- **Parameters**:
  - `token: string`
  - `thing: string`
- **Return Type**: `string`
### `MissingToken(token: string, thing: string): string`

<details><summary>Code</summary>

```ts
(token: string, thing: string) =>
    `Expected to find a ${token} for the ${thing}.`
```
</details>

- **Parameters**:
  - `token: string`
  - `thing: string`
- **Return Type**: `string`
### `nullThrows(value: T, message: string): NonNullable<T>`

<details><summary>Code</summary>

```ts
export function nullThrows<T>(value: T, message: string): NonNullable<T> {
  if (value == null) {
    throw new Error(`Non-null Assertion Failed: ${message}`);
  }

  return value;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Assert that a value must not be null or undefined.
 * This is a nice explicit alternative to the non-null assertion operator.
 */
```

- **Parameters**:
  - `value: T`
  - `message: string`
- **Return Type**: `NonNullable<T>`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---