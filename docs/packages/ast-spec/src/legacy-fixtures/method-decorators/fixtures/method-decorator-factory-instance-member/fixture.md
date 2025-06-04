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
📂 **`packages/ast-spec/src/legacy-fixtures/method-decorators/fixtures/method-decorator-factory-instance-member/fixture.ts`**

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@onlyRead` | `B.instanceMethod` | method | false |


---

## Functions

### `B.instanceMethod(): void`

<details><summary>Code</summary>

```ts
@onlyRead(false)
  instanceMethod() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `B`

<details><summary>Class Code</summary>

```ts
class B {
  @onlyRead(false)
  instanceMethod() {}
}
```
</details>

#### Methods

##### `instanceMethod(): void`

<details><summary>Code</summary>

```ts
@onlyRead(false)
  instanceMethod() {}
```
</details>


---