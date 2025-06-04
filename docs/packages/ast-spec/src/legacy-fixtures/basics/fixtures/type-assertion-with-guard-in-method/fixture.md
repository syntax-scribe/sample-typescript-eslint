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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/type-assertion-with-guard-in-method/fixture.ts`**

## Functions

### `AssertsFoo.isBar(): asserts this is string`

<details><summary>Code</summary>

```ts
isBar(): asserts this is string {
    return;
  }
```
</details>

- **Return Type**: `asserts this is string`

---

## Classes

### `AssertsFoo`

<details><summary>Class Code</summary>

```ts
class AssertsFoo {
  isBar(): asserts this is string {
    return;
  }
  isBaz = (): asserts this is string => {
    return;
  };
}
```
</details>

#### Methods

##### `isBar(): asserts this is string`

<details><summary>Code</summary>

```ts
isBar(): asserts this is string {
    return;
  }
```
</details>


---