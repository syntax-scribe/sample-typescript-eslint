[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `class-fields.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📊 Variables & Constants | 10 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/eslint-scope/class-fields.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `ScopeType` | `../../src/index.js` |
| `parseAndAnalyze` | `../test-utils/index.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `globalScope` | `Scope` | const | `scopeManager.scopes[0]` | ✗ |
| `classScope` | `Scope` | const | `globalScope.childScopes[0]` | ✗ |
| `classFieldInitializerScope` | `Scope` | const | `classScope.childScopes[0]` | ✗ |
| `globalScope` | `Scope` | const | `scopeManager.scopes[0]` | ✗ |
| `classScope` | `Scope` | const | `globalScope.childScopes[0]` | ✗ |
| `globalScope` | `Scope` | const | `scopeManager.scopes[0]` | ✗ |
| `classScope` | `Scope` | const | `globalScope.childScopes[0]` | ✗ |
| `globalScope` | `Scope` | const | `scopeManager.scopes[0]` | ✗ |
| `classScope` | `Scope` | const | `globalScope.childScopes[0]` | ✗ |
| `classFieldInitializerScope` | `Scope` | const | `classScope.childScopes[0]` | ✗ |


---