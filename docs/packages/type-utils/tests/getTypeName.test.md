[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getTypeName.test.ts`

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
📂 **`packages/type-utils/tests/getTypeName.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `getTypeName` | `../src/index.js` |
| `parseCodeForEslint` | `./test-utils/custom-matchers/custom-matchers.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `declaration` | `TSESTree.TSTypeAliasDeclaration` | const | `ast.body[0] as TSESTree.TSTypeAliasDeclaration` | ✗ |


---

## Functions

### `getTypes(code: string): { checker: ts.TypeChecker; type: ts.Type }`

<details><summary>Code</summary>

```ts
function getTypes(code: string): { checker: ts.TypeChecker; type: ts.Type } {
    const { ast, services } = parseCodeForEslint(code);
    const checker = services.program.getTypeChecker();
    const declaration = ast.body[0] as TSESTree.TSTypeAliasDeclaration;

    return { checker, type: services.getTypeAtLocation(declaration.id) };
  }
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `{ checker: ts.TypeChecker; type: ts.Type }`
- **Calls**:
  - `parseCodeForEslint (from ./test-utils/custom-matchers/custom-matchers.js)`
  - `services.program.getTypeChecker`
  - `services.getTypeAtLocation`

---