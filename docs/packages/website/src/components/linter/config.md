[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `config.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/website/src/components/linter/config.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParseSettings` | `@typescript-eslint/typescript-estree/use-at-your-own-risk` |
| `ClassicConfig` | `@typescript-eslint/utils/ts-eslint` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `PARSER_NAME` | `"@typescript-eslint/parser"` | const | `'@typescript-eslint/parser'` | ✓ |
| `defaultParseSettings` | `ParseSettings` | const | `{
  allowInvalidAST: false,
  code: '',
  codeFullText: '',
  comment: true,
  comments: [],
  debugLevel: new Set(),
  errorOnTypeScriptSyntacticAndSemanticIssues: false,
  errorOnUnknownASTType: false,
  extraFileExtensions: [],
  filePath: '',
  // JSDocParsingMode was added in TS 5.3.
  // eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
  jsDocParsingMode: window.ts?.JSDocParsingMode?.ParseAll,
  jsx: true,
  loc: true,
  log: console.log,
  preserveNodeMaps: true,
  programs: null,
  projects: new Map(),
  projectService: undefined,
  range: true,
  singleRun: false,
  suppressDeprecatedPropertyWarnings: false,
  tokens: [],
  tsconfigMatchCache: new Map(),
  tsconfigRootDir: '/',
}` | ✓ |
| `defaultEslintConfig` | `ClassicConfig.Config` | const | `{
  parser: PARSER_NAME,
  parserOptions: {
    ecmaFeatures: {
      globalReturn: false,
      jsx: true,
    },
    ecmaVersion: 'latest',
    project: ['./tsconfig.json'],
    sourceType: 'module',
  },
  rules: {},
}` | ✓ |


---