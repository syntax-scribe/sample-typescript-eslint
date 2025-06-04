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
📂 **`packages/ast-spec/src/legacy-fixtures/parameter-decorators/fixtures/parameter-decorator-decorator-instance-member/fixture.ts`**

## Functions

### `Foo.bar(baz: number): void`

<details><summary>Code</summary>

```ts
bar(@special(true) baz: number) {}
```
</details>

- **Parameters**:
  - `baz: number`
- **Return Type**: `void`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  bar(@special(true) baz: number) {}
}
```
</details>

#### Methods

##### `bar(baz: number): void`

<details><summary>Code</summary>

```ts
bar(@special(true) baz: number) {}
```
</details>


---