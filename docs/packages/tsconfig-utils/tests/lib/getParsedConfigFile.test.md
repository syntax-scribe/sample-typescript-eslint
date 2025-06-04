[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getParsedConfigFile.test.ts`

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
📂 **`packages/tsconfig-utils/tests/lib/getParsedConfigFile.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `path` | `node:path` |
| `getParsedConfigFile` | `../../src/getParsedConfigFile` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `mockTsserver` | `typeof ts` | const | `{
  formatDiagnostics: ts.formatDiagnostics,
  getParsedCommandLineOfConfigFile: mockGetParsedCommandLineOfConfigFile,
  sys: {} as ts.System,
  // eslint-disable-next-line @typescript-eslint/no-explicit-any
} as any` | ✗ |
| `parsedConfigFile` | `{ errors: any[]; options: { strict: boolean; }; raw: { compilerOptions: { strict: boolean; }; }; }` | const | `{
      errors: [],
      options: { strict: true },
      raw: { compilerOptions: { strict: true } },
    }` | ✗ |


---


---