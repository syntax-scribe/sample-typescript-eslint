[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/parameter/AssignmentPattern/fixtures/decorated-assignment-pattern-parameter/fixture.ts`**

## Functions

### `decorator(): void`

<details><summary>Code</summary>

```ts
function decorator() {}
```
</details>

- **Return Type**: `void`
### `A.foo(d: number): void`

<details><summary>Code</summary>

```ts
foo(@decorator d = 1) {}
```
</details>

- **Parameters**:
  - `d: number`
- **Return Type**: `void`

---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  foo(@decorator d = 1) {}
}
```
</details>

#### Methods

##### `foo(d: number): void`

<details><summary>Code</summary>

```ts
foo(@decorator d = 1) {}
```
</details>


---