[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `typeFlagUtils.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---