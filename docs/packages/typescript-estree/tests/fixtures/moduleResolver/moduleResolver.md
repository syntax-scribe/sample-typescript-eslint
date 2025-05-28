[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `moduleResolver.js`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
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

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/typescript-estree/tests/fixtures/moduleResolver/moduleResolver.js`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `resolvedModules` | `any[]` | let/var | `[]` | ✗ |
| `parsedModuleName` | `any` | let/var | `moduleName` | ✗ |


---

## Functions

### `resolveModuleNames(moduleNames: any, containingFile: any, _reusedNames: any, _redirectedReferences: any, compilerOptions: any): any[]`

<details><summary>Code</summary>

```ts
(
    moduleNames,
    containingFile,
    _reusedNames,
    _redirectedReferences,
    compilerOptions,
  ) => {
    const resolvedModules = [];

    for (const moduleName of moduleNames) {
      let parsedModuleName = moduleName;

      if (parsedModuleName === '__PLACEHOLDER__') {
        parsedModuleName = './something';
      }

      const resolution = ts.resolveModuleName(
        parsedModuleName,
        containingFile,
        compilerOptions,
        {
          fileExists: ts.sys.fileExists,
          readFile: ts.sys.readFile,
        },
      );

      resolvedModules.push(resolution.resolvedModule);
    }

    return resolvedModules;
  }
```
</details>

- **Parameters**:
  - `moduleNames: any`
  - `containingFile: any`
  - `_reusedNames: any`
  - `_redirectedReferences: any`
  - `compilerOptions: any`
- **Return Type**: `any[]`
- **Calls**:
  - `ts.resolveModuleName`
  - `resolvedModules.push`
### `resolveModuleNames(moduleNames: any, containingFile: any, _reusedNames: any, _redirectedReferences: any, compilerOptions: any): any[]`

<details><summary>Code</summary>

```ts
(
    moduleNames,
    containingFile,
    _reusedNames,
    _redirectedReferences,
    compilerOptions,
  ) => {
    const resolvedModules = [];

    for (const moduleName of moduleNames) {
      let parsedModuleName = moduleName;

      if (parsedModuleName === '__PLACEHOLDER__') {
        parsedModuleName = './something';
      }

      const resolution = ts.resolveModuleName(
        parsedModuleName,
        containingFile,
        compilerOptions,
        {
          fileExists: ts.sys.fileExists,
          readFile: ts.sys.readFile,
        },
      );

      resolvedModules.push(resolution.resolvedModule);
    }

    return resolvedModules;
  }
```
</details>

- **Parameters**:
  - `moduleNames: any`
  - `containingFile: any`
  - `_reusedNames: any`
  - `_redirectedReferences: any`
  - `compilerOptions: any`
- **Return Type**: `any[]`
- **Calls**:
  - `ts.resolveModuleName`
  - `resolvedModules.push`

---