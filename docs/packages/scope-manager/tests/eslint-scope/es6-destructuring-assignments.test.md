[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `es6-destructuring-assignments.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 38 |
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
📂 **`packages/scope-manager/tests/eslint-scope/es6-destructuring-assignments.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `Reference` | `../../src/index.js` |
| `DefinitionType` | `../../src/index.js` |
| `ScopeType` | `../../src/index.js` |
| `getRealVariables` | `../test-utils/index.js` |
| `parseAndAnalyze` | `../test-utils/index.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `expectedVariableNames` | `string[]` | const | `['arguments', 'a', 'b', 'c', 'd', 'rest']` | ✗ |
| `expectedReferenceNames` | `string[]` | const | `['a', 'b', 'c', 'd', 'rest']` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `expectedVariableNames` | `string[]` | const | `[
      'arguments',
      'shorthand',
      'a',
      'b',
      'c',
      'd',
      'e',
      'world',
    ]` | ✗ |
| `expectedReferenceNames` | `string[]` | const | `[
      'shorthand',
      'a',
      'b',
      'c',
      'd',
      'e',
      'world',
    ]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `expectedReferenceNames` | `string[]` | const | `['a', 'b', 'c', 'd', 'rest']` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `expectedReferenceNames` | `string[]` | const | `[
      'shorthand',
      'a',
      'b',
      'c',
      'd',
      'e',
      'world',
    ]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `expectedVariableNames` | `string[]` | const | `[
      'arguments',
      'shorthand',
      'a',
      'b',
      'c',
      'd',
      'e',
      'world',
    ]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `expectedVariableNames` | `string[]` | const | `['arguments', 'a', 'b', 'c', 'd']` | ✗ |
| `expectedReferenceNames` | `string[]` | const | `[
      'a',
      'b',
      'c',
      'd', // assign 20
      'd', // assign array
      'array',
    ]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `expectedVariableNames` | `string[]` | const | `['arguments', 'a', 'b', 'c', 'd']` | ✗ |
| `expectedReferenceNames` | `string[]` | const | `[
      'a', // assign array
      'b', // assign array
      'c', // assign array
      'd', // assign e
      'd', // assign array
      'e',
      'array',
    ]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `expectedVariableNames` | `string[]` | const | `['arguments', 'a', 'b', 'c', 'd']` | ✗ |
| `expectedReferenceNames` | `string[]` | const | `[
      'a', // assign array
      'b', // assign array
      'c', // assign f
      'c', // assign array
      'd', // assign f
      'd', // assign e
      'd', // assign array
      'e',
      'f',
      'array',
    ]` | ✗ |


---


---