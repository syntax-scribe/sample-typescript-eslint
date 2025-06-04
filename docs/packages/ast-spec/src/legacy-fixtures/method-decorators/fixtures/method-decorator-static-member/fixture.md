[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |
| ✨ Decorators | 1 |

## 📚 Table of Contents

- [Decorators](#decorators)
- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/method-decorators/fixtures/method-decorator-static-member/fixture.ts`**

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@Foo` | `D.staticMethod` | method | *none* |


---

## Functions

### `D.staticMethod(): void`

<details><summary>Code</summary>

```ts
@Foo
  static staticMethod() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `D`

<details><summary>Class Code</summary>

```ts
class D {
  @Foo
  static staticMethod() {}
}
```
</details>

#### Methods

##### `staticMethod(): void`

<details><summary>Code</summary>

```ts
@Foo
  static staticMethod() {}
```
</details>


---