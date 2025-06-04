[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getConstraintInfo.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📊 Variables & Constants | 24 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/util/getConstraintInfo.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserOptions` | `@typescript-eslint/parser` |
| `TSESTree` | `@typescript-eslint/utils` |
| `parseForESLint` | `@typescript-eslint/parser` |
| `getConstraintInfo` | `../../src/util/getConstraintInfo.js` |
| `getFixturesRootDir` | `../RuleTester.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `DEFAULT_PARSER_OPTIONS` | `ParserOptions` | const | `{
  disallowAutomaticSingleRunInference: true,
  filePath: path.join(FIXTURES_DIR, 'file.ts'),
  project: './tsconfig.json',
  tsconfigRootDir: FIXTURES_DIR,
} as const satisfies ParserOptions` | ✗ |
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
| `sourceCode` | `"\nfunction foo<T>() {\n  function bar<V extends T>(x: V) {\n  }\n}\n    "` | const | ``
function foo<T>() {
  function bar<V extends T>(x: V) {
  }
}
    `` | ✗ |
| `outerFunctionNode` | `TSESTree.FunctionDeclaration` | const | `ast.body[0] as TSESTree.FunctionDeclaration` | ✗ |
| `innerFunctionNode` | `TSESTree.FunctionDeclaration` | const | `outerFunctionNode.body
      .body[0] as TSESTree.FunctionDeclaration` | ✗ |
| `parameterNode` | `any` | const | `innerFunctionNode.params[0]` | ✗ |


---