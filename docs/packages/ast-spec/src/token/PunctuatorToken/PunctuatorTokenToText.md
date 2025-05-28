[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `PunctuatorTokenToText.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

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

## 🔧 Functions

> No functions found in this file.


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