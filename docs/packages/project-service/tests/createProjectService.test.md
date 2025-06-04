[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `createProjectService.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📊 Variables & Constants | 7 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/project-service/tests/createProjectService.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `debug` | `debug` |
| `createProjectService` | `../src/createProjectService.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `actual` | `any` | let/var | `await importOriginal()` | ✗ |
| `service` | `any` | const | `projectServiceSettings.service as typeof projectServiceSettings.service & {
            eventHandler: ts.server.ProjectServiceEventHandler | undefined;
          }` | ✗ |
| `allowDefaultProject` | `string[]` | const | `['./*.js']` | ✗ |
| `compilerOptions` | `ts.CompilerOptions` | const | `{ strict: true }` | ✗ |
| `defaultProject` | `"tsconfig.eslint.json"` | const | `'tsconfig.eslint.json'` | ✗ |
| `compilerOptions` | `ts.CompilerOptions` | let/var | `{ strict: true }` | ✗ |
| `tsconfigRootDir` | `"path/to/repo"` | let/var | `'path/to/repo'` | ✗ |


---