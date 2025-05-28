[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `method.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |
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
📂 **`packages/scope-manager/tests/fixtures/class/declaration/method.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `unresolved1` | `{ (): any; <T>(): void; <T extends object = object>(): void; (): void; (a: number): number; (): void; (a: number): void; (): void; (a: number): void; <T>(): void; (a: number): number; (): void; (): void; }` | const | `f` | ✗ |
| `unresolved2` | `any` | const | `method` | ✗ |


---

## Functions

### `A.method(a: any, [b]: any, { c }: any, d: number, e: any, f: any): void`

<details><summary>Code</summary>

```ts
method(a, [b], { c }, d = 1, e = a, f) {
    a;
  }
```
</details>

- **Parameters**:
  - `a: any`
  - `[b]: any`
  - `{ c }: any`
  - `d: number`
  - `e: any`
  - `f: any`
- **Return Type**: `void`

---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  method(a, [b], { c }, d = 1, e = a, f) {
    a;
  }
}
```
</details>

#### Methods

##### `method(a: any, [b]: any, { c }: any, d: number, e: any, f: any): void`

<details><summary>Code</summary>

```ts
method(a, [b], { c }, d = 1, e = a, f) {
    a;
  }
```
</details>


---