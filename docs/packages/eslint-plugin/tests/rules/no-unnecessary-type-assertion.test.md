[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-type-assertion.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/no-unnecessary-type-assertion.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `path` | `node:path` |
| `rule` | `../../src/rules/no-unnecessary-type-assertion` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      project: './tsconfig.json',
      projectService: false,
      tsconfigRootDir: rootDir,
    },
  },
})` | ✗ |
| `optionsWithOnUncheckedIndexedAccess` | `{ project: string; tsconfigRootDir: string; }` | const | `{
  project: './tsconfig.noUncheckedIndexedAccess.json',
  tsconfigRootDir: rootDir,
}` | ✗ |
| `optionsWithExactOptionalPropertyTypes` | `{ project: string; tsconfigRootDir: string; }` | const | `{
  project: './tsconfig.exactOptionalPropertyTypes.json',
  tsconfigRootDir: rootDir,
}` | ✗ |


---