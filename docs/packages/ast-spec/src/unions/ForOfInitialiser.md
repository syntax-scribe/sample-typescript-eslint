[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ForOfInitialiser.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/ForOfInitialiser.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `LetOrConstOrVarDeclaration` | `../declaration/VariableDeclaration/spec` |
| `UsingInForOfDeclaration` | `../declaration/VariableDeclaration/spec` |
| `Expression` | `./Expression` |


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

### `ForOfInitialiser`

```ts
type ForOfInitialiser = | Expression
  | LetOrConstOrVarDeclaration
  | UsingInForOfDeclaration;
```


---