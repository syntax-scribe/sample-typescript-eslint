[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `AssignmentOperatorToText.test-d.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/AssignmentOperatorToText.test-d.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AssignmentOperator` | `typescript` |
| `AssignmentOperatorToText` | `../src` |


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

### `_Test`

```ts
type _Test = {
    readonly [T in AssignmentOperator]: AssignmentOperatorToText[T];
    // If there are any AssignmentOperator members that don't have a corresponding
    // AssignmentOperatorToText, then this line will error with "Type 'T' cannot
    // be used to index type 'AssignmentOperatorToText'."
  };
```


---