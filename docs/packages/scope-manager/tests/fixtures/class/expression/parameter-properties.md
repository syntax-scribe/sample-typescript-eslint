[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `parameter-properties.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 3 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/class/expression/parameter-properties.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `outer` | `1` | const | `1` | ✗ |
| `A` | `typeof A` | const | `class {
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
}` | ✗ |
| `unresovled` | `any` | const | `e` | ✗ |


---


---

## Type Aliases

### `Outer`

```ts
type Outer = 1;
```


---