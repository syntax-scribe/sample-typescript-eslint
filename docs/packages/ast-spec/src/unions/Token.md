[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Token.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 13
- **Interfaces**: 0
- **Type Aliases**: 1

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

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


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