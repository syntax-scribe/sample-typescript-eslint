[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `no-unused-vars.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 2 |
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

## 🔧 Functions

> No functions found in this file.


---