[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `PunctuatorTokenToText.test-d.ts`

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
📂 **`packages/ast-spec/tests/PunctuatorTokenToText.test-d.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `PunctuationSyntaxKind` | `typescript` |
| `PunctuatorTokenToText` | `../src` |


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
    readonly [T in PunctuationSyntaxKind]: PunctuatorTokenToText[T];
    // If there are any PunctuationSyntaxKind members that don't have a
    // corresponding PunctuatorTokenToText, then this line will error with
    // "Type 'T' cannot be used to index type 'PunctuatorTokenToText'."
  };
```


---