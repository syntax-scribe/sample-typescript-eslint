[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `type-predicate2.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/functions/function-declaration/type-predicate2.ts`**

## Functions

### `foo(arg: any): arg is T`

<details><summary>Code</summary>

```ts
function foo(arg: any): arg is T {
  return typeof arg === 'string';
}
```
</details>

- **Parameters**:
  - `arg: any`
- **Return Type**: `arg is T`

---

## Type Aliases

### `T`

```ts
type T = string;
```


---