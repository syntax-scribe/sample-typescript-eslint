[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `visitor-keys.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/visitor-keys/tests/visitor-keys.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `visitorKeys` | `../src` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `types` | `Set<string>` | const | `new Set(Object.keys(AST_NODE_TYPES))` | ✗ |
| `keys` | `Set<string>` | const | `new Set(Object.keys(visitorKeys))` | ✗ |
| `IGNORED_KEYS` | `Set<string>` | const | `new Set([
  'ExperimentalRestProperty',
  'ExperimentalSpreadProperty',
])` | ✗ |


---