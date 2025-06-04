[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `es6-default-parameters.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 30 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/eslint-scope/es6-default-parameters.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `getRealVariables` | `../test-utils/index.js` |
| `parseAndAnalyze` | `../test-utils/index.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `patterns` | `readonly [readonly [any, "let foo = (a, b = 0) => {};"], readonly [any, "function foo(a, b = 0) {}"], readonly [any, "let foo = function(a, b = 0) {};"]]` | const | `[
      [AST_NODE_TYPES.ArrowFunctionExpression, 'let foo = (a, b = 0) => {};'],
      [AST_NODE_TYPES.FunctionDeclaration, 'function foo(a, b = 0) {}'],
      [AST_NODE_TYPES.FunctionExpression, 'let foo = function(a, b = 0) {};'],
    ] as const` | ✗ |
| `numVars` | `2 | 3` | const | `name === AST_NODE_TYPES.ArrowFunctionExpression ? 2 : 3` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[1]` | ✗ |
| `reference` | `Reference` | const | `scope.references[0]` | ✗ |
| `patterns` | `readonly [readonly [any, "\n        let a;\n        let foo = (b = a) => {};\n      "], readonly [any, "\n        let a;\n        function foo(b = a) {}\n      "], readonly [any, "\n        let a;\n        let foo = function(b = a) {}\n      "]]` | const | `[
      [
        AST_NODE_TYPES.ArrowFunctionExpression,
        `
        let a;
        let foo = (b = a) => {};
      `,
      ],
      [
        AST_NODE_TYPES.FunctionDeclaration,
        `
        let a;
        function foo(b = a) {}
      `,
      ],
      [
        AST_NODE_TYPES.FunctionExpression,
        `
        let a;
        let foo = function(b = a) {}
      `,
      ],
    ] as const` | ✗ |
| `numVars` | `1 | 2` | const | `name === AST_NODE_TYPES.ArrowFunctionExpression ? 1 : 2` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[1]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `patterns` | `readonly [readonly [any, "\n        const a = 0;\n        let foo = (b = a) => {};\n      "], readonly [any, "\n        const a = 0;\n        function foo(b = a) {}\n      "], readonly [any, "\n        const a = 0;\n        let foo = function(b = a) {}\n      "]]` | const | `[
      [
        AST_NODE_TYPES.ArrowFunctionExpression,
        `
        const a = 0;
        let foo = (b = a) => {};
      `,
      ],
      [
        AST_NODE_TYPES.FunctionDeclaration,
        `
        const a = 0;
        function foo(b = a) {}
      `,
      ],
      [
        AST_NODE_TYPES.FunctionExpression,
        `
        const a = 0;
        let foo = function(b = a) {}
      `,
      ],
    ] as const` | ✗ |
| `numVars` | `1 | 2` | const | `name === AST_NODE_TYPES.ArrowFunctionExpression ? 1 : 2` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[1]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `patterns` | `readonly [readonly [any, "\n        let a;\n        let foo = (b = a.c) => {};\n      "], readonly [any, "\n        let a;\n        function foo(b = a.c) {}\n      "], readonly [any, "\n        let a;\n        let foo = function(b = a.c) {}\n      "]]` | const | `[
      [
        AST_NODE_TYPES.ArrowFunctionExpression,
        `
        let a;
        let foo = (b = a.c) => {};
      `,
      ],
      [
        AST_NODE_TYPES.FunctionDeclaration,
        `
        let a;
        function foo(b = a.c) {}
      `,
      ],
      [
        AST_NODE_TYPES.FunctionExpression,
        `
        let a;
        let foo = function(b = a.c) {}
      `,
      ],
    ] as const` | ✗ |
| `numVars` | `1 | 2` | const | `name === AST_NODE_TYPES.ArrowFunctionExpression ? 1 : 2` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[1]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `patterns` | `readonly [readonly [any, "\n        let a;\n        let foo = (b = function() { return a; }) => {};\n      "], readonly [any, "\n        let a;\n        function foo(b = function() { return a; }) {}\n      "], readonly [...]]` | const | `[
      [
        AST_NODE_TYPES.ArrowFunctionExpression,
        `
        let a;
        let foo = (b = function() { return a; }) => {};
      `,
      ],
      [
        AST_NODE_TYPES.FunctionDeclaration,
        `
        let a;
        function foo(b = function() { return a; }) {}
      `,
      ],
      [
        AST_NODE_TYPES.FunctionExpression,
        `
        let a;
        let foo = function(b = function() { return a; }) {}
      `,
      ],
    ] as const` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[2]` | ✗ |
| `reference` | `Reference` | const | `scope.references[0]` | ✗ |
| `patterns` | `readonly [readonly [any, "\n        let a;\n        let foo = (b = a) => { let a; };\n      "], readonly [any, "\n        let a;\n        function foo(b = a) { let a; }\n      "], readonly [any, "\n        let a;\n        let foo = function(b = a) { let a; }\n      "]]` | const | `[
      [
        AST_NODE_TYPES.ArrowFunctionExpression,
        `
        let a;
        let foo = (b = a) => { let a; };
      `,
      ],
      [
        AST_NODE_TYPES.FunctionDeclaration,
        `
        let a;
        function foo(b = a) { let a; }
      `,
      ],
      [
        AST_NODE_TYPES.FunctionExpression,
        `
        let a;
        let foo = function(b = a) { let a; }
      `,
      ],
    ] as const` | ✗ |
| `numVars` | `2 | 3` | const | `name === AST_NODE_TYPES.ArrowFunctionExpression ? 2 : 3` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[1]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `patterns` | `readonly [readonly [any, "\n        let a;\n        let foo = (b = a, a) => { };\n      "], readonly [any, "\n        let a;\n        function foo(b = a, a) { }\n      "], readonly [any, "\n        let a;\n        let foo = function(b = a, a) { }\n      "]]` | const | `[
      [
        AST_NODE_TYPES.ArrowFunctionExpression,
        `
        let a;
        let foo = (b = a, a) => { };
      `,
      ],
      [
        AST_NODE_TYPES.FunctionDeclaration,
        `
        let a;
        function foo(b = a, a) { }
      `,
      ],
      [
        AST_NODE_TYPES.FunctionExpression,
        `
        let a;
        let foo = function(b = a, a) { }
      `,
      ],
    ] as const` | ✗ |
| `numVars` | `2 | 3` | const | `name === AST_NODE_TYPES.ArrowFunctionExpression ? 2 : 3` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[1]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `patterns` | `readonly [readonly [any, "\n        let a;\n        let foo = (b = function(){ a }) => { let a; };\n      "], readonly [any, "\n        let a;\n        function foo(b = function(){ a }) { let a; }\n      "], readonly [...]]` | const | `[
      [
        AST_NODE_TYPES.ArrowFunctionExpression,
        `
        let a;
        let foo = (b = function(){ a }) => { let a; };
      `,
      ],
      [
        AST_NODE_TYPES.FunctionDeclaration,
        `
        let a;
        function foo(b = function(){ a }) { let a; }
      `,
      ],
      [
        AST_NODE_TYPES.FunctionExpression,
        `
        let a;
        let foo = function(b = function(){ a }) { let a; }
      `,
      ],
    ] as const` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[2]` | ✗ |
| `reference` | `Reference` | const | `scope.references[0]` | ✗ |


---


---