[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `AssignmentOperatorToText.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
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
📂 **`packages/ast-spec/src/expression/AssignmentExpression/AssignmentOperatorToText.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `SyntaxKind` | `typescript` |


---

## 🔧 Functions

> No functions found in this file.


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