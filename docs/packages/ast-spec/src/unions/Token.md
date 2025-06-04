[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Token.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 13 |
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
📂 **`packages/ast-spec/src/unions/Token.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `BooleanToken` | `../token/BooleanToken/spec` |
| `IdentifierToken` | `../token/IdentifierToken/spec` |
| `JSXIdentifierToken` | `../token/JSXIdentifierToken/spec` |
| `JSXTextToken` | `../token/JSXTextToken/spec` |
| `KeywordToken` | `../token/KeywordToken/spec` |
| `NullToken` | `../token/NullToken/spec` |
| `NumericToken` | `../token/NumericToken/spec` |
| `PrivateIdentifierToken` | `../token/PrivateIdentifierToken/spec` |
| `PunctuatorToken` | `../token/PunctuatorToken/spec` |
| `RegularExpressionToken` | `../token/RegularExpressionToken/spec` |
| `StringToken` | `../token/StringToken/spec` |
| `TemplateToken` | `../token/TemplateToken/spec` |
| `Comment` | `./Comment` |


---


---

## Type Aliases

### `Token`

```ts
type Token = | BooleanToken
  | Comment
  | IdentifierToken
  | JSXIdentifierToken
  | JSXTextToken
  | KeywordToken
  | NullToken
  | NumericToken
  | PrivateIdentifierToken
  | PunctuatorToken
  | RegularExpressionToken
  | StringToken
  | TemplateToken;
```


---