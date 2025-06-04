[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `index.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📊 Variables & Constants | 2 |
| 🔄 Re-exports | 2 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Re-exports](#re-exports)

## 🛠️ File Location:
📂 **`packages/parser/src/index.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `version` | `string` | const | `require('../package.json').version` | ✓ |
| `meta` | `{ name: string; version: string; }` | const | `{
  name: 'typescript-eslint/parser',
  version,
}` | ✓ |


---

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| named | `./parser` | parse, parseForESLint, ParserOptions |
| named | `@typescript-eslint/typescript-estree` | clearCaches, createProgram, ParserServices, ParserServicesWithoutTypeInformation, ParserServicesWithTypeInformation, withoutProjectParserOptions |


---