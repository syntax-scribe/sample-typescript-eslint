[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ESLint.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
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
📂 **`packages/utils/tests/ts-eslint/ESLint.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `FlatESLint` | `eslint/use-at-your-own-risk` |
| `LegacyESLint` | `eslint/use-at-your-own-risk` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `eslint` | `FlatESLint` | const | `new ESLint.FlatESLint({
        // accepts flat configs
        baseConfig: [{ ignores: [] }, { languageOptions: {} }],
        overrideConfig: [{ ignores: [] }, { languageOptions: {} }],
      })` | ✗ |
| `eslint` | `LegacyESLint` | const | `new ESLint.LegacyESLint({
        // accepts legacy configs
        baseConfig: {
          overrides: [],
          parserOptions: {},
        },
        overrideConfig: {
          overrides: [],
          parserOptions: {},
        },
      })` | ✗ |


---

## 🔧 Functions

> No functions found in this file.


---