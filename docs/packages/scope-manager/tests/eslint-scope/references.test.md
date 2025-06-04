[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `references.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 37 |
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
📂 **`packages/scope-manager/tests/eslint-scope/references.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `getRealVariables` | `../test-utils/index.js` |
| `parseAndAnalyze` | `../test-utils/index.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `scope` | `Scope` | const | `scopeManager.scopes[0]` | ✗ |
| `reference` | `Reference` | const | `scope.references[0]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[1]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[1]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[0]` | ✗ |
| `reference` | `Reference` | const | `scope.references[0]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[1]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[0]` | ✗ |
| `reference` | `Reference` | const | `scope.references[0]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[1]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[0]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[2]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[1]` | ✗ |
| `reference` | `Reference` | const | `scope.references[0]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[2]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[1]` | ✗ |
| `reference` | `Reference` | const | `scope.references[0]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[2]` | ✗ |
| `reference` | `Reference` | const | `scope.references[1]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[0]` | ✗ |
| `reference` | `Reference` | const | `scope.references[0]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[0]` | ✗ |
| `reference` | `Reference` | const | `scope.references[0]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[0]` | ✗ |
| `reference` | `Reference` | const | `scope.references[0]` | ✗ |
| `trueCodes` | `readonly ["var a = 0;", "let a = 0;", "const a = 0;", "var [a] = [];", "let [a] = [];", "const [a] = [];", "var [a = 1] = [];", "let [a = 1] = [];", "const [a = 1] = [];", ... 21 more ..., "new function({b: a = 0} = {}) {}"]` | const | `[
      'var a = 0;',
      'let a = 0;',
      'const a = 0;',
      'var [a] = [];',
      'let [a] = [];',
      'const [a] = [];',
      'var [a = 1] = [];',
      'let [a = 1] = [];',
      'const [a = 1] = [];',
      'var {a} = {};',
      'let {a} = {};',
      'const {a} = {};',
      'var {b: a} = {};',
      'let {b: a} = {};',
      'const {b: a} = {};',
      'var {b: a = 0} = {};',
      'let {b: a = 0} = {};',
      'const {b: a = 0} = {};',
      'for (var a in []);',
      'for (let a in []);',
      'for (var [a] in []);',
      'for (let [a] in []);',
      'for (var [a = 0] in []);',
      'for (let [a = 0] in []);',
      'for (var {a} in []);',
      'for (let {a} in []);',
      'for (var {a = 0} in []);',
      'for (let {a = 0} in []);',
      'new function(a = 0) {}',
      'new function([a = 0] = []) {}',
      'new function({b: a = 0} = {}) {}',
    ] as const` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[scopeManager.scopes.length - 1]` | ✗ |
| `falseCodes` | `readonly ["let a; a = 0;", "let a; [a] = [];", "let a; [a = 1] = [];", "let a; ({a} = {});", "let a; ({b: a} = {});", "let a; ({b: a = 0} = {});", "let a; for (a in []);", "let a; for ([a] in []);", "let a; for ([a = 0] in []);", "let a; for ({a} in []);", "let a; for ({a = 0} in []);"]` | const | `[
      'let a; a = 0;',
      'let a; [a] = [];',
      'let a; [a = 1] = [];',
      'let a; ({a} = {});',
      'let a; ({b: a} = {});',
      'let a; ({b: a = 0} = {});',
      'let a; for (a in []);',
      'let a; for ([a] in []);',
      'let a; for ([a = 0] in []);',
      'let a; for ({a} in []);',
      'let a; for ({a = 0} in []);',
    ] as const` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[scopeManager.scopes.length - 1]` | ✗ |
| `scope` | `Scope` | const | `scopeManager.scopes[0]` | ✗ |


---


---