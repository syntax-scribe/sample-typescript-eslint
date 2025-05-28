[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `nullThrows.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/utils/src/eslint-utils/nullThrows.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `NullThrowsReasons` | `{ readonly MissingParent: "Expected node to have a parent."; readonly MissingToken: (token: string, thing: string) => string; }` | const | `{
  MissingParent: 'Expected node to have a parent.',
  MissingToken: (token: string, thing: string) =>
    `Expected to find a ${token} for the ${thing}.`,
} as const` | ✓ |


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