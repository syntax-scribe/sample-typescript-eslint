[⬅️ Back to Table of Contents](../../../../../../../index.md)

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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-with-generic-method-default/fixture.ts`**

## Functions

### `Foo.getBar(): void`

<details><summary>Code</summary>

```ts
getBar<T = Bar>() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  getBar<T = Bar>() {}
}
```
</details>

#### Methods

##### `getBar(): void`

<details><summary>Code</summary>

```ts
getBar<T = Bar>() {}
```
</details>


---