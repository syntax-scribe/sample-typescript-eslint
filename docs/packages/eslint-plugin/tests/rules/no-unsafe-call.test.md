[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unsafe-call.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/no-unsafe-call.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `rule` | `../../src/rules/no-unsafe-call` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      project: './tsconfig.noImplicitThis.json',
      projectService: false,
      tsconfigRootDir: getFixturesRootDir(),
    },
  },
})` | ✗ |


---