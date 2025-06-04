[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `AssignmentOperatorToText.test-d.ts`

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
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/AssignmentOperatorToText.test-d.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AssignmentOperator` | `typescript` |
| `AssignmentOperatorToText` | `../src` |


---


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