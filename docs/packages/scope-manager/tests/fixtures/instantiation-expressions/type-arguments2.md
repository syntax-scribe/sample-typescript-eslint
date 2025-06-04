[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `type-arguments2.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 1 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/instantiation-expressions/type-arguments2.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `makeStringBox` | `(value: string) => { value: string; }` | const | `makeBox<string>` | ✗ |


---

## Functions

### `makeBox(value: T): { value: T; }`

<details><summary>Code</summary>

```ts
function makeBox<T>(value: T) {
  return { value };
}
```
</details>

- **Parameters**:
  - `value: T`
- **Return Type**: `{ value: T; }`

---

## Type Aliases

### `BoxFunc<T>`

```ts
type BoxFunc<T> = typeof makeBox<T>;
```


---