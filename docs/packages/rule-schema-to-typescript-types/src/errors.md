[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `errors.ts`

## 📚 Table of Contents

- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 2
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-schema-to-typescript-types/src/errors.ts`**

## 📦 Imports

> No imports found in this file.


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

### `NotSupportedError`

<details><summary>Class Code</summary>

```ts
export class NotSupportedError extends Error {
  constructor(thing: string, target: unknown) {
    super(
      `Generating a type for ${thing} is not currently supported:\n${JSON.stringify(
        target,
        null,
        2,
      )}`,
    );
  }
}
```
</details>

### `UnexpectedError`

<details><summary>Class Code</summary>

```ts
export class UnexpectedError extends Error {
  constructor(error: string, target: unknown) {
    super(`Unexpected Error: ${error}:\n${JSON.stringify(target, null, 2)}`);
  }
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