[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `params.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/functions/function-expression/params.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `outer` | `1` | const | `1` | ✗ |
| `unresolved` | `<T extends typeof g>(g: T) => number` | const | `g` | ✗ |


---

## Functions

### `foo(a: any, [b]: any, { c }: any, d: number, e: any, f: number, g: any): void`

<details><summary>Code</summary>

```ts
function (a, [b], { c }, d = 1, e = a, f = outer, g) {
  a;
}
```
</details>

- **Parameters**:
  - `a: any`
  - `[b]: any`
  - `{ c }: any`
  - `d: number`
  - `e: any`
  - `f: number`
  - `g: any`
- **Return Type**: `void`

---