[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Literal.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/Literal.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `BigIntLiteral` | `../expression/literal/BigIntLiteral/spec` |
| `BooleanLiteral` | `../expression/literal/BooleanLiteral/spec` |
| `NullLiteral` | `../expression/literal/NullLiteral/spec` |
| `NumberLiteral` | `../expression/literal/NumberLiteral/spec` |
| `RegExpLiteral` | `../expression/literal/RegExpLiteral/spec` |
| `StringLiteral` | `../expression/literal/StringLiteral/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Type Aliases

### `Literal`

```ts
type Literal = | BigIntLiteral
  | BooleanLiteral
  | NullLiteral
  | NumberLiteral
  | RegExpLiteral
  | StringLiteral;
```


---