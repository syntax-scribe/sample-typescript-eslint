[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getTypeName.test.ts`

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
📂 **`packages/type-utils/tests/getTypeName.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `getTypeName` | `../src/index.js` |
| `parseCodeForEslint` | `./test-utils/custom-matchers/custom-matchers.js` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---