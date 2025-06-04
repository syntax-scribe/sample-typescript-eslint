[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `isSymbolFromDefaultLibrary.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/tests/isSymbolFromDefaultLibrary.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/typescript-estree` |
| `isSymbolFromDefaultLibrary` | `../src/index.js` |
| `parseCodeForEslint` | `./test-utils/custom-matchers/custom-matchers.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `declaration` | `TSESTree.TSTypeAliasDeclaration` | const | `ast.body[0] as TSESTree.TSTypeAliasDeclaration` | ✗ |


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