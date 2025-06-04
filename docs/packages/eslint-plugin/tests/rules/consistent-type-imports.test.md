[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `consistent-type-imports.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📊 Variables & Constants | 3 |

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