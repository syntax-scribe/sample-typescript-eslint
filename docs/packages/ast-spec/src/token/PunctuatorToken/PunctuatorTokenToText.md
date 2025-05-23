[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `PunctuatorTokenToText.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/token/PunctuatorToken/PunctuatorTokenToText.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `SyntaxKind` | `typescript` |
| `AssignmentOperatorToText` | `../../expression/AssignmentExpression/AssignmentOperatorToText` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `PunctuatorTokenToText`

<details><summary>Interface Code</summary>

```ts
export interface PunctuatorTokenToText extends AssignmentOperatorToText {
  [SyntaxKind.AmpersandAmpersandToken]: '&&';
  [SyntaxKind.AmpersandToken]: '&';
  [SyntaxKind.AsteriskAsteriskToken]: '**';
  [SyntaxKind.AsteriskToken]: '*';
  [SyntaxKind.AtToken]: '@';
  [SyntaxKind.BacktickToken]: '`';
  [SyntaxKind.BarBarToken]: '||';
  [SyntaxKind.BarToken]: '|';
  [SyntaxKind.CaretToken]: '^';
  [SyntaxKind.CloseBraceToken]: '}';
  [SyntaxKind.CloseBracketToken]: ']';
  [SyntaxKind.CloseParenToken]: ')';
  [SyntaxKind.ColonToken]: ':';
  [SyntaxKind.CommaToken]: ',';
  [SyntaxKind.DotDotDotToken]: '...';
  [SyntaxKind.DotToken]: '.';
  [SyntaxKind.EqualsEqualsEqualsToken]: '===';
  [SyntaxKind.EqualsEqualsToken]: '==';
  [SyntaxKind.EqualsGreaterThanToken]: '=>';
  [SyntaxKind.ExclamationEqualsEqualsToken]: '!==';
  [SyntaxKind.ExclamationEqualsToken]: '!=';
  [SyntaxKind.ExclamationToken]: '!';
  [SyntaxKind.GreaterThanEqualsToken]: '>=';
  [SyntaxKind.GreaterThanGreaterThanGreaterThanToken]: '>>>';
  [SyntaxKind.GreaterThanGreaterThanToken]: '>>';
  [SyntaxKind.GreaterThanToken]: '>';
  [SyntaxKind.HashToken]: '#';
  [SyntaxKind.LessThanEqualsToken]: '<=';
  [SyntaxKind.LessThanLessThanToken]: '<<';
  [SyntaxKind.LessThanSlashToken]: '</';
  [SyntaxKind.LessThanToken]: '<';
  [SyntaxKind.MinusMinusToken]: '--';
  [SyntaxKind.MinusToken]: '-';
  [SyntaxKind.OpenBraceToken]: '{';
  [SyntaxKind.OpenBracketToken]: '[';
  [SyntaxKind.OpenParenToken]: '(';
  [SyntaxKind.PercentToken]: '%';
  [SyntaxKind.PlusPlusToken]: '++';
  [SyntaxKind.PlusToken]: '+';
  [SyntaxKind.QuestionDotToken]: '?.';
  [SyntaxKind.QuestionQuestionToken]: '??';
  [SyntaxKind.QuestionToken]: '?';
  [SyntaxKind.SemicolonToken]: ';';
  [SyntaxKind.SlashToken]: '/';
  [SyntaxKind.TildeToken]: '~';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `[SyntaxKind.AmpersandAmpersandToken]` | `'&&'` | ✗ |  |
| `[SyntaxKind.AmpersandToken]` | `'&'` | ✗ |  |
| `[SyntaxKind.AsteriskAsteriskToken]` | `'**'` | ✗ |  |
| `[SyntaxKind.AsteriskToken]` | `'*'` | ✗ |  |
| `[SyntaxKind.AtToken]` | `'@'` | ✗ |  |
| `[SyntaxKind.BacktickToken]` | `'`'` | ✗ |  |
| `[SyntaxKind.BarBarToken]` | `'||'` | ✗ |  |
| `[SyntaxKind.BarToken]` | `'|'` | ✗ |  |
| `[SyntaxKind.CaretToken]` | `'^'` | ✗ |  |
| `[SyntaxKind.CloseBraceToken]` | `'}'` | ✗ |  |
| `[SyntaxKind.CloseBracketToken]` | `']'` | ✗ |  |
| `[SyntaxKind.CloseParenToken]` | `')'` | ✗ |  |
| `[SyntaxKind.ColonToken]` | `':'` | ✗ |  |
| `[SyntaxKind.CommaToken]` | `','` | ✗ |  |
| `[SyntaxKind.DotDotDotToken]` | `'...'` | ✗ |  |
| `[SyntaxKind.DotToken]` | `'.'` | ✗ |  |
| `[SyntaxKind.EqualsEqualsEqualsToken]` | `'==='` | ✗ |  |
| `[SyntaxKind.EqualsEqualsToken]` | `'=='` | ✗ |  |
| `[SyntaxKind.EqualsGreaterThanToken]` | `'=>'` | ✗ |  |
| `[SyntaxKind.ExclamationEqualsEqualsToken]` | `'!=='` | ✗ |  |
| `[SyntaxKind.ExclamationEqualsToken]` | `'!='` | ✗ |  |
| `[SyntaxKind.ExclamationToken]` | `'!'` | ✗ |  |
| `[SyntaxKind.GreaterThanEqualsToken]` | `'>='` | ✗ |  |
| `[SyntaxKind.GreaterThanGreaterThanGreaterThanToken]` | `'>>>'` | ✗ |  |
| `[SyntaxKind.GreaterThanGreaterThanToken]` | `'>>'` | ✗ |  |
| `[SyntaxKind.GreaterThanToken]` | `'>'` | ✗ |  |
| `[SyntaxKind.HashToken]` | `'#'` | ✗ |  |
| `[SyntaxKind.LessThanEqualsToken]` | `'<='` | ✗ |  |
| `[SyntaxKind.LessThanLessThanToken]` | `'<<'` | ✗ |  |
| `[SyntaxKind.LessThanSlashToken]` | `'</'` | ✗ |  |
| `[SyntaxKind.LessThanToken]` | `'<'` | ✗ |  |
| `[SyntaxKind.MinusMinusToken]` | `'--'` | ✗ |  |
| `[SyntaxKind.MinusToken]` | `'-'` | ✗ |  |
| `[SyntaxKind.OpenBraceToken]` | `'{'` | ✗ |  |
| `[SyntaxKind.OpenBracketToken]` | `'['` | ✗ |  |
| `[SyntaxKind.OpenParenToken]` | `'('` | ✗ |  |
| `[SyntaxKind.PercentToken]` | `'%'` | ✗ |  |
| `[SyntaxKind.PlusPlusToken]` | `'++'` | ✗ |  |
| `[SyntaxKind.PlusToken]` | `'+'` | ✗ |  |
| `[SyntaxKind.QuestionDotToken]` | `'?.'` | ✗ |  |
| `[SyntaxKind.QuestionQuestionToken]` | `'??'` | ✗ |  |
| `[SyntaxKind.QuestionToken]` | `'?'` | ✗ |  |
| `[SyntaxKind.SemicolonToken]` | `';'` | ✗ |  |
| `[SyntaxKind.SlashToken]` | `'/'` | ✗ |  |
| `[SyntaxKind.TildeToken]` | `'~'` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---