[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `typeof-this.ts`

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
📂 **`packages/scope-manager/tests/fixtures/decorators/typeof-this.ts`**

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@decorator` | `Foo` | class | *none* |


---

## Functions

### `decorator(): void`

<details><summary>Code</summary>

```ts
function decorator() {}
```
</details>

- **Return Type**: `void`
### `Foo.bar(baz: typeof this): void`

<details><summary>Code</summary>

```ts
bar(baz: typeof this) {}
```
</details>

- **Parameters**:
  - `baz: typeof this`
- **Return Type**: `void`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
@decorator
class Foo {
  bar(baz: typeof this) {}
}
```
</details>

#### Methods

##### `bar(baz: typeof this): void`

<details><summary>Code</summary>

```ts
bar(baz: typeof this) {}
```
</details>


---