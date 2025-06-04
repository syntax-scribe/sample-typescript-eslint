[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `accessor.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/decorators/accessor.ts`**

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
  @decorator
  get foo() {
    return 1;
  }
  @decorator
  set bar(value) {}
}
```
</details>


---