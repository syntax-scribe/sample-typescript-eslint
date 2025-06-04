[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Literal.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 6 |
| 📑 Type Aliases | 1 |

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