[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `parameter-property.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/decorators/parameter-property.ts`**

## Functions

### `decorator(): void`

<details><summary>Code</summary>

```ts
function decorator() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  constructor(
    @decorator readonly a,
    @decorator readonly b = 1,
  ) {}
}
```
</details>


---