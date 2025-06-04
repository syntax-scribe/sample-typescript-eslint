[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `method.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 1 |
| ✨ Decorators | 1 |

## 📚 Table of Contents

- [Decorators](#decorators)
- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/decorators/method.ts`**

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@decorator` | `Foo.foo` | method | *none* |


---

## Functions

### `decorator(): void`

<details><summary>Code</summary>

```ts
function decorator() {}
```
</details>

- **Return Type**: `void`
### `Foo.foo(): void`

<details><summary>Code</summary>

```ts
@decorator
  foo() {}
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
  foo() {}
}
```
</details>

#### Methods

##### `foo(): void`

<details><summary>Code</summary>

```ts
@decorator
  foo() {}
```
</details>


---