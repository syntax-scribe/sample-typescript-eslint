[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `deprecated.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 3
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/fixtures/deprecated.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `deprecatedFunction(): void`

<details><summary>Code</summary>

```ts
export function deprecatedFunction(): void {}
```
</details>

- **JSDoc**:
```ts
/** @deprecated */
```

- **Return Type**: `void`
### `normalFunction(): void`

<details><summary>Code</summary>

```ts
function normalFunction(): void;
```
</details>

- **Return Type**: `void`
### `deprecatedFunctionWithOverloads(): void`

<details><summary>Code</summary>

```ts
function deprecatedFunctionWithOverloads(): void;
```
</details>

- **Return Type**: `void`

---

## Classes

### `DeprecatedClass`

<details><summary>Class Code</summary>

```ts
export class DeprecatedClass {
  /** @deprecated */
  foo: string = '';
}
```
</details>

### `NormalClass`

<details><summary>Class Code</summary>

```ts
class NormalClass {}
```
</details>

### `ClassWithDeprecatedConstructor`

<details><summary>Class Code</summary>

```ts
export class ClassWithDeprecatedConstructor {
  constructor();
  /** @deprecated */
  constructor(arg: string);
  constructor(arg?: string) {}
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