[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-useless-empty-export.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/no-useless-empty-export.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `rule` | `../../src/rules/no-useless-empty-export` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      ecmaVersion: 2020,
      sourceType: 'module',
    },
  },
})` | ✗ |
| `error` | `{ readonly messageId: "uselessExport"; }` | const | `{
  messageId: 'uselessExport',
} as const` | ✗ |


---