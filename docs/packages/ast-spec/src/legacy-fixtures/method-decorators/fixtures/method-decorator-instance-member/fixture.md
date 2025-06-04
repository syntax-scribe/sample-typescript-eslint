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
📂 **`packages/ast-spec/src/legacy-fixtures/method-decorators/fixtures/method-decorator-instance-member/fixture.ts`**

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@onlyRead` | `A.instanceMethod` | method | *none* |


---

## Functions

### `A.instanceMethod(): void`

<details><summary>Code</summary>

```ts
@onlyRead
  instanceMethod() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  @onlyRead
  instanceMethod() {}
}
```
</details>

#### Methods

##### `instanceMethod(): void`

<details><summary>Code</summary>

```ts
@onlyRead
  instanceMethod() {}
```
</details>


---