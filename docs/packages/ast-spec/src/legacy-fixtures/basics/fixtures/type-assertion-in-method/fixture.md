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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/type-assertion-in-method/fixture.ts`**

## Functions

### `AssertsFoo.isBar(): asserts this`

<details><summary>Code</summary>

```ts
isBar(): asserts this {
    return;
  }
```
</details>

- **Return Type**: `asserts this`

---

## Classes

### `AssertsFoo`

<details><summary>Class Code</summary>

```ts
class AssertsFoo {
  isBar(): asserts this {
    return;
  }
  isBaz = (): asserts this => {
    return;
  };
}
```
</details>

#### Methods

##### `isBar(): asserts this`

<details><summary>Code</summary>

```ts
isBar(): asserts this {
    return;
  }
```
</details>


---