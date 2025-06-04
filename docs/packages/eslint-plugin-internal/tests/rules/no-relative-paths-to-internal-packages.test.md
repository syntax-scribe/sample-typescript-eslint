[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-relative-paths-to-internal-packages.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin-internal/tests/rules/no-relative-paths-to-internal-packages.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `path` | `node:path` |
| `PACKAGES_DIR` | `../../src/rules/no-relative-paths-to-internal-packages` |
| `rule` | `../../src/rules/no-relative-paths-to-internal-packages` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      tsconfigRootDir: PACKAGES_DIR,
    },
  },
})` | ✗ |


---