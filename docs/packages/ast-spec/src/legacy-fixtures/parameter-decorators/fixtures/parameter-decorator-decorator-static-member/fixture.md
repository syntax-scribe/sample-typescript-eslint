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
📂 **`packages/ast-spec/src/legacy-fixtures/parameter-decorators/fixtures/parameter-decorator-decorator-static-member/fixture.ts`**

## Functions

### `StaticFoo.bar(baz: number): void`

<details><summary>Code</summary>

```ts
static bar(@special(true) baz: number) {}
```
</details>

- **Parameters**:
  - `baz: number`
- **Return Type**: `void`

---

## Classes

### `StaticFoo`

<details><summary>Class Code</summary>

```ts
class StaticFoo {
  static bar(@special(true) baz: number) {}
}
```
</details>

#### Methods

##### `bar(baz: number): void`

<details><summary>Code</summary>

```ts
static bar(@special(true) baz: number) {}
```
</details>


---