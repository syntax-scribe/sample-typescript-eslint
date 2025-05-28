[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `options.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
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

## 🔧 Functions

> No functions found in this file.


---