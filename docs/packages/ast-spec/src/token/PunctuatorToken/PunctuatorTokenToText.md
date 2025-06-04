[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `PunctuatorTokenToText.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/token/PunctuatorToken/PunctuatorTokenToText.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `SyntaxKind` | `typescript` |
| `AssignmentOperatorToText` | `../../expression/AssignmentExpression/AssignmentOperatorToText` |


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