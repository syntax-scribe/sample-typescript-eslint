[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `type-query-with-parameters.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/type-query-with-parameters.ts`**

## Functions

### `foo(y: T): { y: T; }`

<details><summary>Code</summary>

```ts
function foo<T>(y: T) {
  return { y };
}
```
</details>

- **Parameters**:
  - `y: T`
- **Return Type**: `{ y: T; }`

---

## Type Aliases

### `Foo<T>`

```ts
type Foo<T> = typeof foo<T>;
```


---