[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `discriminateAnyType.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/type-utils/tests/discriminateAnyType.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/typescript-estree` |
| `AnyType` | `../src/index.js` |
| `discriminateAnyType` | `../src/index.js` |
| `parseCodeForEslint` | `./test-utils/custom-matchers/custom-matchers.js` |


---

## Functions

### `getDeclarationId(ast: TSESTree.Program): TSESTree.Node`

<details><summary>Code</summary>

```ts
function getDeclarationId(ast: TSESTree.Program): TSESTree.Node {
    const declaration = ast.body.at(-1) as TSESTree.VariableDeclaration;
    const { id } = declaration.declarations[0];
    return id;
  }
```
</details>

- **Parameters**:
  - `ast: TSESTree.Program`
- **Return Type**: `TSESTree.Node`
- **Calls**:
  - `ast.body.at`
### `getTypes(code: string, getNode: GetNode): { checker: any; program: any; tsNode: any; type: any; }`

<details><summary>Code</summary>

```ts
function getTypes(code: string, getNode: GetNode) {
    const { ast, services } = parseCodeForEslint(code);
    const node = getNode(ast);
    const type = services.getTypeAtLocation(getNode(ast));
    return {
      checker: services.program.getTypeChecker(),
      program: services.program,
      tsNode: services.esTreeNodeToTSNodeMap.get(node),
      type,
    };
  }
```
</details>

- **Parameters**:
  - `code: string`
  - `getNode: GetNode`
- **Return Type**: `{ checker: any; program: any; tsNode: any; type: any; }`
- **Calls**:
  - `parseCodeForEslint (from ./test-utils/custom-matchers/custom-matchers.js)`
  - `getNode`
  - `services.getTypeAtLocation`
  - `services.program.getTypeChecker`
  - `services.esTreeNodeToTSNodeMap.get`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `GetNode`

```ts
type GetNode = (ast: TSESTree.Program) => TSESTree.Node;
```


---