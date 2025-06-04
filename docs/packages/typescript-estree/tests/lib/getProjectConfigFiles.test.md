[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getProjectConfigFiles.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 7 |
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
📂 **`packages/typescript-estree/tests/lib/getProjectConfigFiles.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `existsSync` | `node:fs` |
| `path` | `node:path` |
| `ExpiringCache` | `../../src/parseSettings/ExpiringCache` |
| `getProjectConfigFiles` | `../../src/parseSettings/getProjectConfigFiles` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `actual` | `any` | let/var | `await importOriginal()` | ✗ |
| `parseSettings` | `{ filePath: string; tsconfigMatchCache: ExpiringCache<string, string>; tsconfigRootDir: string; }` | const | `{
  filePath: './repos/repo/packages/package/file.ts',
  tsconfigMatchCache: new ExpiringCache<string, string>(1),
  tsconfigRootDir: './repos/repo',
}` | ✗ |
| `project` | `"./tsconfig.eslint.json"` | const | `'./tsconfig.eslint.json'` | ✗ |
| `project` | `string[]` | const | `['./tsconfig.eslint.json']` | ✗ |
| `testCases` | `readonly [readonly [any], readonly [any], readonly [false]]` | const | `[[undefined], [null], [false]] as const` | ✗ |
| `tsconfigMatchCache` | `ExpiringCache<string, string>` | const | `new ExpiringCache<string, string>(1)` | ✗ |
| `tsconfigMatchCache` | `ExpiringCache<string, string>` | const | `new ExpiringCache<string, string>(1)` | ✗ |


---


---