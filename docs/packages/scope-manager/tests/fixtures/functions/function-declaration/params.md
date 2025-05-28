[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `params.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 2 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/functions/function-declaration/params.ts`**

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
function foo(a, [b], { c }, d = 1, e = a, f = outer, g) {
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