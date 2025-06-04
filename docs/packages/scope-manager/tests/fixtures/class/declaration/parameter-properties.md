[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `parameter-properties.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📊 Variables & Constants | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Classes](#classes)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/class/declaration/parameter-properties.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `outer` | `1` | const | `1` | ✗ |
| `unresovled` | `any` | const | `e` | ✗ |


---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  constructor(
    private a,
    private b = 1,
    private c = a,
    public d = outer,
    public e,
    readonly f: Outer,
  ) {
    a;
  }
}
```
</details>


---

## Type Aliases

### `Outer`

```ts
type Outer = 1;
```


---