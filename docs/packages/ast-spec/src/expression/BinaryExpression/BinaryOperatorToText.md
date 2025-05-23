[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `BinaryOperatorToText.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/BinaryExpression/BinaryOperatorToText.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `SyntaxKind` | `typescript` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---