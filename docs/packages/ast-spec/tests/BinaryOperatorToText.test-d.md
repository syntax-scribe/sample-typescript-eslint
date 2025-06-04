[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `BinaryOperatorToText.test-d.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/BinaryOperatorToText.test-d.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AssignmentOperator` | `typescript` |
| `BinaryOperator` | `typescript` |
| `SyntaxKind` | `typescript` |
| `BinaryOperatorToText` | `../src` |


---


---

## Type Aliases

### `BinaryOperatorWithoutInvalidTypes`

```ts
type BinaryOperatorWithoutInvalidTypes = Exclude<
  BinaryOperator,
  | AssignmentOperator // --> AssignmentExpression
  | SyntaxKind.CommaToken // -> SequenceExpression
  | SyntaxKind.QuestionQuestionToken // -> LogicalExpression
>;
```

### `_Test`

```ts
type _Test = {
    readonly [T in BinaryOperatorWithoutInvalidTypes]: BinaryOperatorToText[T];
    // If there are any BinaryOperator members that don't have a corresponding
    // BinaryOperatorToText, then this line will error with "Type 'T' cannot
    // be used to index type 'BinaryOperatorToText'."
  };
```


---