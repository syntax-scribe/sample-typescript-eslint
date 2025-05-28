[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `consistent-type-imports.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 3 |
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
📂 **`packages/eslint-plugin/tests/rules/consistent-type-imports.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `rule` | `../../src/rules/consistent-type-imports` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `PARSER_OPTION_COMBOS` | `readonly [{ readonly emitDecoratorMetadata: false; readonly experimentalDecorators: false; }, { readonly emitDecoratorMetadata: true; readonly experimentalDecorators: false; }, { readonly emitDecoratorMetadata: false; readonly experimentalDecorators: true; }]` | const | `[
  {
    emitDecoratorMetadata: false,
    experimentalDecorators: false,
  },
  {
    emitDecoratorMetadata: true,
    experimentalDecorators: false,
  },
  {
    emitDecoratorMetadata: false,
    experimentalDecorators: true,
  },
] as const` | ✗ |
| `ruleTester` | `any` | const | `new RuleTester({
      languageOptions: { parserOptions },
    })` | ✗ |
| `ruleTester` | `any` | const | `new RuleTester({
    languageOptions: {
      parserOptions: {
        emitDecoratorMetadata: true,
        experimentalDecorators: true,
      },
    },
  })` | ✗ |


---

## 🔧 Functions

> No functions found in this file.


---