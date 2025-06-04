[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `AssignmentOperatorToText.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 1 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/AssignmentExpression/AssignmentOperatorToText.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `SyntaxKind` | `typescript` |


---

## Interfaces

### `AssignmentOperatorToText`

<details><summary>Interface Code</summary>

```ts
export interface AssignmentOperatorToText {
  [SyntaxKind.AmpersandAmpersandEqualsToken]: '&&=';
  [SyntaxKind.AmpersandEqualsToken]: '&=';
  [SyntaxKind.AsteriskAsteriskEqualsToken]: '**=';
  [SyntaxKind.AsteriskEqualsToken]: '*=';
  [SyntaxKind.BarBarEqualsToken]: '||=';
  [SyntaxKind.BarEqualsToken]: '|=';
  [SyntaxKind.CaretEqualsToken]: '^=';
  [SyntaxKind.EqualsToken]: '=';
  [SyntaxKind.GreaterThanGreaterThanEqualsToken]: '>>=';
  [SyntaxKind.GreaterThanGreaterThanGreaterThanEqualsToken]: '>>>=';
  [SyntaxKind.LessThanLessThanEqualsToken]: '<<=';
  [SyntaxKind.MinusEqualsToken]: '-=';
  [SyntaxKind.PercentEqualsToken]: '%=';
  [SyntaxKind.PlusEqualsToken]: '+=';
  [SyntaxKind.QuestionQuestionEqualsToken]: '??=';
  [SyntaxKind.SlashEqualsToken]: '/=';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `[SyntaxKind.AmpersandAmpersandEqualsToken]` | `'&&='` | ✗ |  |
| `[SyntaxKind.AmpersandEqualsToken]` | `'&='` | ✗ |  |
| `[SyntaxKind.AsteriskAsteriskEqualsToken]` | `'**='` | ✗ |  |
| `[SyntaxKind.AsteriskEqualsToken]` | `'*='` | ✗ |  |
| `[SyntaxKind.BarBarEqualsToken]` | `'||='` | ✗ |  |
| `[SyntaxKind.BarEqualsToken]` | `'|='` | ✗ |  |
| `[SyntaxKind.CaretEqualsToken]` | `'^='` | ✗ |  |
| `[SyntaxKind.EqualsToken]` | `'='` | ✗ |  |
| `[SyntaxKind.GreaterThanGreaterThanEqualsToken]` | `'>>='` | ✗ |  |
| `[SyntaxKind.GreaterThanGreaterThanGreaterThanEqualsToken]` | `'>>>='` | ✗ |  |
| `[SyntaxKind.LessThanLessThanEqualsToken]` | `'<<='` | ✗ |  |
| `[SyntaxKind.MinusEqualsToken]` | `'-='` | ✗ |  |
| `[SyntaxKind.PercentEqualsToken]` | `'%='` | ✗ |  |
| `[SyntaxKind.PlusEqualsToken]` | `'+='` | ✗ |  |
| `[SyntaxKind.QuestionQuestionEqualsToken]` | `'??='` | ✗ |  |
| `[SyntaxKind.SlashEqualsToken]` | `'/='` | ✗ |  |


---