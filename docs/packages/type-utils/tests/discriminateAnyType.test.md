[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `discriminateAnyType.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 5 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `declaration` | `TSESTree.VariableDeclaration` | const | `ast.body.at(-1) as TSESTree.VariableDeclaration` | ✗ |
| `code` | `"\nclass Foo {\n  foo() {\n    return this;\n  }\n  protected then(resolve: () => void): void {\n    resolve();\n  }\n};\n        "` | const | ``
class Foo {
  foo() {
    return this;
  }
  protected then(resolve: () => void): void {
    resolve();
  }
};
        `` | ✗ |
| `classDeclration` | `TSESTree.ClassDeclaration` | const | `ast.body[0] as TSESTree.ClassDeclaration` | ✗ |
| `method` | `TSESTree.MethodDefinition` | const | `classDeclration.body
          .body[0] as TSESTree.MethodDefinition` | ✗ |
| `returnStatement` | `TSESTree.ReturnStatement` | const | `method.value.body?.body.at(
          -1,
        ) as TSESTree.ReturnStatement` | ✗ |


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

## Type Aliases

### `GetNode`

```ts
type GetNode = (ast: TSESTree.Program) => TSESTree.Node;
```


---