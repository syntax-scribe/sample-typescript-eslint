[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `moduleResolver.js`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/tests/fixtures/moduleResolver/moduleResolver.js`**

## 📦 Imports

> No imports found in this file.


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---