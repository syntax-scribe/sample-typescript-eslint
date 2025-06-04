[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `es6-import.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📊 Variables & Constants | 8 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/eslint-scope/es6-import.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
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
| `imports` | `string[]` | const | `[
      'import v from "mod";',
      'import { v } from "mod";',
      'import * as v from "mod";',
    ]` | ✗ |
| `scope` | `Scope` | let/var | `scopeManager.scopes[0]` | ✗ |
| `importV` | `Variable` | const | `variables[0]` | ✗ |
| `variableX` | `Variable` | const | `variables[1]` | ✗ |


---