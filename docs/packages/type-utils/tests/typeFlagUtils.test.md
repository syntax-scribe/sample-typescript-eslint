[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `typeFlagUtils.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/tests/typeFlagUtils.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/typescript-estree` |
| `getTypeFlags` | `../src/index.js` |
| `isTypeFlagSet` | `../src/index.js` |
| `parseCodeForEslint` | `./test-utils/custom-matchers/custom-matchers.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `declaration` | `TSESTree.TSTypeAliasDeclaration` | const | `ast.body[0] as TSESTree.TSTypeAliasDeclaration` | ✗ |


---

## Functions

### `getType(code: string): ts.Type`

<details><summary>Code</summary>

```ts
function getType(code: string): ts.Type {
    const { ast, services } = parseCodeForEslint(code);
    const declaration = ast.body[0] as TSESTree.TSTypeAliasDeclaration;

    return services.getTypeAtLocation(declaration.id);
  }
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `ts.Type`
- **Calls**:
  - `parseCodeForEslint (from ./test-utils/custom-matchers/custom-matchers.js)`
  - `services.getTypeAtLocation`

---