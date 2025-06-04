[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `BinaryOperatorToText.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 1 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/BinaryExpression/BinaryOperatorToText.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `SyntaxKind` | `typescript` |


---

## Interfaces

### `BinaryOperatorToText`

<details><summary>Interface Code</summary>

```ts
export interface BinaryOperatorToText {
  // logical
  [SyntaxKind.AmpersandAmpersandToken]: '&&';
  // bitwise
  [SyntaxKind.AmpersandToken]: '&';

  // math
  [SyntaxKind.AsteriskAsteriskToken]: '**';
  [SyntaxKind.AsteriskToken]: '*';
  [SyntaxKind.BarBarToken]: '||';
  [SyntaxKind.BarToken]: '|';
  [SyntaxKind.CaretToken]: '^';
  [SyntaxKind.EqualsEqualsEqualsToken]: '===';

  [SyntaxKind.EqualsEqualsToken]: '==';
  [SyntaxKind.ExclamationEqualsEqualsToken]: '!==';
  [SyntaxKind.ExclamationEqualsToken]: '!=';
  [SyntaxKind.GreaterThanEqualsToken]: '>=';
  [SyntaxKind.GreaterThanGreaterThanGreaterThanToken]: '>>>';
  [SyntaxKind.GreaterThanGreaterThanToken]: '>>';

  [SyntaxKind.GreaterThanToken]: '>';
  [SyntaxKind.InKeyword]: 'in';
  [SyntaxKind.InstanceOfKeyword]: 'instanceof';
  [SyntaxKind.LessThanEqualsToken]: '<=';
  [SyntaxKind.LessThanLessThanToken]: '<<';
  [SyntaxKind.LessThanToken]: '<';
  [SyntaxKind.MinusToken]: '-';
  [SyntaxKind.PercentToken]: '%';
  [SyntaxKind.PlusToken]: '+';
  [SyntaxKind.SlashToken]: '/';
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
| `[SyntaxKind.BarBarToken]` | `'||'` | ✗ |  |
| `[SyntaxKind.BarToken]` | `'|'` | ✗ |  |
| `[SyntaxKind.CaretToken]` | `'^'` | ✗ |  |
| `[SyntaxKind.EqualsEqualsEqualsToken]` | `'==='` | ✗ |  |
| `[SyntaxKind.EqualsEqualsToken]` | `'=='` | ✗ |  |
| `[SyntaxKind.ExclamationEqualsEqualsToken]` | `'!=='` | ✗ |  |
| `[SyntaxKind.ExclamationEqualsToken]` | `'!='` | ✗ |  |
| `[SyntaxKind.GreaterThanEqualsToken]` | `'>='` | ✗ |  |
| `[SyntaxKind.GreaterThanGreaterThanGreaterThanToken]` | `'>>>'` | ✗ |  |
| `[SyntaxKind.GreaterThanGreaterThanToken]` | `'>>'` | ✗ |  |
| `[SyntaxKind.GreaterThanToken]` | `'>'` | ✗ |  |
| `[SyntaxKind.InKeyword]` | `'in'` | ✗ |  |
| `[SyntaxKind.InstanceOfKeyword]` | `'instanceof'` | ✗ |  |
| `[SyntaxKind.LessThanEqualsToken]` | `'<='` | ✗ |  |
| `[SyntaxKind.LessThanLessThanToken]` | `'<<'` | ✗ |  |
| `[SyntaxKind.LessThanToken]` | `'<'` | ✗ |  |
| `[SyntaxKind.MinusToken]` | `'-'` | ✗ |  |
| `[SyntaxKind.PercentToken]` | `'%'` | ✗ |  |
| `[SyntaxKind.PlusToken]` | `'+'` | ✗ |  |
| `[SyntaxKind.SlashToken]` | `'/'` | ✗ |  |


---