[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/special/TSTypeParameter/fixtures/method-const-modifiers/fixture.ts`**

## Functions

### `_.method(): void`

<details><summary>Code</summary>

```ts
method<const T>() {}
```
</details>

- **Return Type**: `void`
### `_.method(): void`

<details><summary>Code</summary>

```ts
method<const T extends U>() {}
```
</details>

- **Return Type**: `void`
### `_.method(): void`

<details><summary>Code</summary>

```ts
method<T, const U>() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `_`

<details><summary>Class Code</summary>

```ts
class _ {
  method<const T>() {}
  method<const T extends U>() {}
  method<T, const U>() {}
}
```
</details>

#### Methods

##### `method(): void`

<details><summary>Code</summary>

```ts
method<const T>() {}
```
</details>

##### `method(): void`

<details><summary>Code</summary>

```ts
method<const T extends U>() {}
```
</details>

##### `method(): void`

<details><summary>Code</summary>

```ts
method<T, const U>() {}
```
</details>


---