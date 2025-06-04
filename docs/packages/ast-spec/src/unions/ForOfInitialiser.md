[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ForOfInitialiser.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/ForOfInitialiser.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `LetOrConstOrVarDeclaration` | `../declaration/VariableDeclaration/spec` |
| `UsingInForOfDeclaration` | `../declaration/VariableDeclaration/spec` |
| `Expression` | `./Expression` |


---

## Type Aliases

### `ForOfInitialiser`

```ts
type ForOfInitialiser = | Expression
  | LetOrConstOrVarDeclaration
  | UsingInForOfDeclaration;
```


---