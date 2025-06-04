[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getConstrainedTypeAtLocation.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📊 Variables & Constants | 19 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/type-utils/tests/getConstrainedTypeAtLocation.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `getConstrainedTypeAtLocation` | `../src/index.js` |
| `isTypeUnknownType` | `../src/index.js` |
| `parseCodeForEslint` | `./test-utils/custom-matchers/custom-matchers.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `sourceCode` | `"\nfunction foo<T>(x: T);\n    "` | const | ``
function foo<T>(x: T);
    `` | ✗ |
| `functionNode` | `TSESTree.FunctionDeclaration` | const | `ast.body[0] as TSESTree.FunctionDeclaration` | ✗ |
| `parameterNode` | `any` | const | `functionNode.params[0]` | ✗ |
| `sourceCode` | `"\nfunction foo<T extends unknown>(x: T);\n    "` | const | ``
function foo<T extends unknown>(x: T);
    `` | ✗ |
| `functionNode` | `TSESTree.FunctionDeclaration` | const | `ast.body[0] as TSESTree.FunctionDeclaration` | ✗ |
| `parameterNode` | `any` | const | `functionNode.params[0]` | ✗ |
| `sourceCode` | `"\nfunction foo<T extends any>(x: T);\n    "` | const | ``
function foo<T extends any>(x: T);
    `` | ✗ |
| `functionNode` | `TSESTree.FunctionDeclaration` | const | `ast.body[0] as TSESTree.FunctionDeclaration` | ✗ |
| `parameterNode` | `any` | const | `functionNode.params[0]` | ✗ |
| `sourceCode` | `"\nfunction foo<T extends string>(x: T);\n    "` | const | ``
function foo<T extends string>(x: T);
    `` | ✗ |
| `functionNode` | `TSESTree.FunctionDeclaration` | const | `ast.body[0] as TSESTree.FunctionDeclaration` | ✗ |
| `parameterNode` | `any` | const | `functionNode.params[0]` | ✗ |
| `sourceCode` | `"\nfunction foo(x: string);\n    "` | const | ``
function foo(x: string);
    `` | ✗ |
| `functionNode` | `TSESTree.FunctionDeclaration` | const | `ast.body[0] as TSESTree.FunctionDeclaration` | ✗ |
| `parameterNode` | `any` | const | `functionNode.params[0]` | ✗ |
| `sourceCode` | `"\nfunction foo<T extends string>() {\n  function bar<V extends T>(x: V) {\n  }\n}\n    "` | const | ``
function foo<T extends string>() {
  function bar<V extends T>(x: V) {
  }
}
    `` | ✗ |
| `outerFunctionNode` | `TSESTree.FunctionDeclaration` | const | `ast.body[0] as TSESTree.FunctionDeclaration` | ✗ |
| `innerFunctionNode` | `TSESTree.FunctionDeclaration` | const | `outerFunctionNode.body
      .body[0] as TSESTree.FunctionDeclaration` | ✗ |
| `parameterNode` | `any` | const | `innerFunctionNode.params[0]` | ✗ |


---