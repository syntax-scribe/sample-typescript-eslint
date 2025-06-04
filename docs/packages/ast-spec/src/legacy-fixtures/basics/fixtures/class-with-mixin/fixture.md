[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 2 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-with-mixin/fixture.ts`**

## Functions

### `M(Base: T): { new (...args: any[]): (Anonymous class); prototype: M<any>.(Anonymous class); } & T`

<details><summary>Code</summary>

```ts
function M<T extends Constructor<{}>>(Base: T) {
  return class extends Base {};
}
```
</details>

- **Parameters**:
  - `Base: T`
- **Return Type**: `{ new (...args: any[]): (Anonymous class); prototype: M<any>.(Anonymous class); } & T`

---

## Classes

### `X`

<details><summary>Class Code</summary>

```ts
class X extends M<any>(C) implements I {}
```
</details>

### `C`

<details><summary>Class Code</summary>

```ts
class C {}
```
</details>


---

## Interfaces

### `I`

<details><summary>Interface Code</summary>

```ts
interface I {}
```
</details>


---

## Type Aliases

### `Constructor<T>`

```ts
type Constructor<T> = new (...args: any[]) => T;
```


---