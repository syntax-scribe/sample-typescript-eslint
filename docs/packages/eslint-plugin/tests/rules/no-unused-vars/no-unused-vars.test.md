[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `no-unused-vars.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/no-unused-vars/no-unused-vars.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `rule` | `../../../src/rules/no-unused-vars` |
| `collectVariables` | `../../../src/util` |
| `getFixturesRootDir` | `../../RuleTester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      ecmaFeatures: {},
      ecmaVersion: 6,
      sourceType: 'module',
    },
  },
})` | ✗ |
| `withMetaParserOptions` | `{ project: string; projectService: boolean; tsconfigRootDir: string; }` | const | `{
  project: './tsconfig-withmeta.json',
  projectService: false,
  tsconfigRootDir: getFixturesRootDir(),
}` | ✗ |


---