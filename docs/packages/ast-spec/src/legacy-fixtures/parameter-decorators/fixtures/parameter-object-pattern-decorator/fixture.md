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
📂 **`packages/ast-spec/src/legacy-fixtures/parameter-decorators/fixtures/parameter-object-pattern-decorator/fixture.ts`**

## Functions

### `Foo.bar({ bar }: any): void`

<details><summary>Code</summary>

```ts
bar(@special(true) { bar }: any) {}
```
</details>

- **Parameters**:
  - `{ bar }: any`
- **Return Type**: `void`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  bar(@special(true) { bar }: any) {}
}
```
</details>

#### Methods

##### `bar({ bar }: any): void`

<details><summary>Code</summary>

```ts
bar(@special(true) { bar }: any) {}
```
</details>


---