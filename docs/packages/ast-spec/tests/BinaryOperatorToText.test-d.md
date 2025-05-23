[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `BinaryOperatorToText.test-d.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 2

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