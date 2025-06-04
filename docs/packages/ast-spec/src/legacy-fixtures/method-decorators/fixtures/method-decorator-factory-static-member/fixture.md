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
📂 **`packages/ast-spec/src/legacy-fixtures/method-decorators/fixtures/method-decorator-factory-static-member/fixture.ts`**

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@Foo` | `C.staticMethod` | method | false |


---

## Functions

### `C.staticMethod(): void`

<details><summary>Code</summary>

```ts
@Foo(false)
  static staticMethod() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `C`

<details><summary>Class Code</summary>

```ts
class C {
  @Foo(false)
  static staticMethod() {}
}
```
</details>

#### Methods

##### `staticMethod(): void`

<details><summary>Code</summary>

```ts
@Foo(false)
  static staticMethod() {}
```
</details>


---