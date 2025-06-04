[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `PunctuatorTokenToText.test-d.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/PunctuatorTokenToText.test-d.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `PunctuationSyntaxKind` | `typescript` |
| `PunctuatorTokenToText` | `../src` |


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