[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `parameter.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 1 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/decorators/parameter.ts`**

## Functions

### `decorator(): void`

<details><summary>Code</summary>

```ts
function decorator() {}
```
</details>

- **Return Type**: `void`
### `A.foo(a: any, [b]: any, { c }: any, d: number, decorator: any, decorator: any): void`

<details><summary>Code</summary>

```ts
foo(
    @decorator a,
    @decorator [b],
    @decorator { c },
    @decorator d = 1,
    @decorator decorator,
    @d decorator,
  ) {}
```
</details>

- **Parameters**:
  - `a: any`
  - `[b]: any`
  - `{ c }: any`
  - `d: number`
  - `decorator: any`
  - `decorator: any`
- **Return Type**: `void`

---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  foo(
    @decorator a,
    @decorator [b],
    @decorator { c },
    @decorator d = 1,
    @decorator decorator,
    @d decorator,
  ) {}
}
```
</details>

#### Methods

##### `foo(a: any, [b]: any, { c }: any, d: number, decorator: any, decorator: any): void`

<details><summary>Code</summary>

```ts
foo(
    @decorator a,
    @decorator [b],
    @decorator { c },
    @decorator d = 1,
    @decorator decorator,
    @d decorator,
  ) {}
```
</details>


---