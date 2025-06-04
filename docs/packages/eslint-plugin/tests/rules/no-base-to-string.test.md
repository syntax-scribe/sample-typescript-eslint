[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-base-to-string.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📊 Variables & Constants | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/no-base-to-string.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `rule` | `../../src/rules/no-base-to-string` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      project: './tsconfig.json',
      tsconfigRootDir: rootDir,
    },
  },
})` | ✗ |
| `literalListBasic` | `string[]` | const | `[
  "''",
  "'text'",
  'true',
  'false',
  '1',
  '1n',
  '[]',
  '/regex/',
]` | ✗ |
| `literalListNeedParen` | `string[]` | const | `[
  "__dirname === 'foobar'",
  '{}.constructor()',
  '() => {}',
  'function() {}',
]` | ✗ |
| `literalList` | `string[]` | const | `[...literalListBasic, ...literalListNeedParen]` | ✗ |
| `literalListWrapped` | `string[]` | const | `[
  ...literalListBasic,
  ...literalListNeedParen.map(i => `(${i})`),
]` | ✗ |


---