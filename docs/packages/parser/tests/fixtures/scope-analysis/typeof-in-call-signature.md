[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `typeof-in-call-signature.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

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