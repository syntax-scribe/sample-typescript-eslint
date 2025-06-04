[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `typeof-in-call-signature.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📊 Variables & Constants | 1 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/typeof-in-call-signature.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `obj` | `{ value: number; }` | const | `{ value: 1 }` | ✗ |


---

## Interfaces

### `A`

<details><summary>Interface Code</summary>

```ts
interface A {
  <T extends typeof obj>(a: typeof obj, b: T): typeof obj;
  new <T extends typeof obj>(a: typeof obj, b: T): typeof obj;
}
```
</details>


---