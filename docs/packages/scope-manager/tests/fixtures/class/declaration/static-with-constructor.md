[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `static-with-constructor.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/class/declaration/static-with-constructor.ts`**

## Functions

### `f(): void`

<details><summary>Code</summary>

```ts
function f() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  static {}

  constructor() {
    f();
  }
}
```
</details>


---