[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `isSymbolFromDefaultLibrary.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/tests/isSymbolFromDefaultLibrary.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/typescript-estree` |
| `isSymbolFromDefaultLibrary` | `../src/index.js` |
| `parseCodeForEslint` | `./test-utils/custom-matchers/custom-matchers.js` |


---

## Functions

### `getTypes(code: string): {
    program: ts.Program;
    symbol: ts.Symbol | undefined;
  }`

<details><summary>Code</summary>

```ts
function getTypes(code: string): {
    program: ts.Program;
    symbol: ts.Symbol | undefined;
  } {
    const { ast, services } = parseCodeForEslint(code);
    const declaration = ast.body[0] as TSESTree.TSTypeAliasDeclaration;
    const type = services.getTypeAtLocation(declaration.id);
    return { program: services.program, symbol: type.getSymbol() };
  }
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `{
    program: ts.Program;
    symbol: ts.Symbol | undefined;
  }`
- **Calls**:
  - `parseCodeForEslint (from ./test-utils/custom-matchers/custom-matchers.js)`
  - `services.getTypeAtLocation`
  - `type.getSymbol`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---