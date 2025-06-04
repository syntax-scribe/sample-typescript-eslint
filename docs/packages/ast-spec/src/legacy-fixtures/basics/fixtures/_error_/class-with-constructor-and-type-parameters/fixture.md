[⬅️ Back to Table of Contents](../../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/_error_/class-with-constructor-and-type-parameters/fixture.ts`**

## Functions

### `C.['constructor'](): void`

<details><summary>Code</summary>

```ts
['constructor']<T>() { }
```
</details>

- **Return Type**: `void`

---

## Classes

### `C`

<details><summary>Class Code</summary>

```ts
class C {
  constructor<T>() { }

  ['constructor']<T>() { }
}
```
</details>

#### Methods

##### `['constructor'](): void`

<details><summary>Code</summary>

```ts
['constructor']<T>() { }
```
</details>


---