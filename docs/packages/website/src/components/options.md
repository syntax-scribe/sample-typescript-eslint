[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `options.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/website/src/components/options.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ConfigFileType` | `./types` |
| `ConfigModel` | `./types` |
| `ConfigShowAst` | `./types` |
| `toJson` | `./lib/json` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `detailTabs` | `{ label: string; value: ConfigShowAst }[]` | const | `[
  { label: 'Errors', value: false },
  { label: 'ESTree', value: 'es' },
  { label: 'TypeScript', value: 'ts' },
  { label: 'Scope', value: 'scope' },
  { label: 'Types', value: 'types' },
]` | ✓ |
| `fileTypes` | `ConfigFileType[]` | const | `[
  '.ts',
  '.tsx',
  '.js',
  '.jsx',
  '.d.ts',
  '.cjs',
  '.mjs',
  '.cts',
  '.mts',
]` | ✓ |
| `defaultConfig` | `ConfigModel` | const | `{
  code: '',
  eslintrc: toJson({
    rules: {},
  }),
  fileType: '.tsx',
  scroll: true,
  showAST: false,
  showTokens: false,
  sourceType: 'module',
  ts: process.env.TS_VERSION,
  tsconfig: toJson({
    compilerOptions: {
      strictNullChecks: true,
    },
  }),
}` | ✓ |


---