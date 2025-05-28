[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `deprecated.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 3 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 2 |
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
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/fixtures/deprecated.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `deprecatedVariable` | `1` | const | `1` | ✓ |
| `normalVariable` | `1` | const | `1` | ✗ |


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