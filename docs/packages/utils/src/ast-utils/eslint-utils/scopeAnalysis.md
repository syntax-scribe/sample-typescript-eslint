[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `scopeAnalysis.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 1 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/utils/src/ast-utils/eslint-utils/scopeAnalysis.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `../../ts-estree` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `findVariable` | `(initialScope: scopeManager.Scope, nameOrNode: any) => any` | const | `eslintUtils.findVariable as (
  initialScope: TSESLint.Scope.Scope,
  nameOrNode: string | TSESTree.Identifier,
) => TSESLint.Scope.Variable | null` | ✓ |
| `getInnermostScope` | `(initialScope: scopeManager.Scope, node: TSESTree.Node) => scopeManager.Scope` | const | `eslintUtils.getInnermostScope as (
  initialScope: TSESLint.Scope.Scope,
  node: TSESTree.Node,
) => TSESLint.Scope.Scope` | ✓ |


---