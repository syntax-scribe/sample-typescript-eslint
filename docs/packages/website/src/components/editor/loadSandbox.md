[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `loadSandbox.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 1 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Async/Await Patterns](#asyncawait-patterns)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/website/src/components/editor/loadSandbox.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `MonacoEditor` | `monaco-editor` |
| `WebLinterModule` | `../linter/types` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `instance` | `Promise<SandboxModel> | undefined` | let/var | `*not shown*` | ✗ |


---

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| promise-chain | `loadSandbox` | *none* | new Promise(...) |


---

## Functions

### `loadSandbox(tsVersion: string): Promise<SandboxModel>`

<details><summary>Code</summary>

```ts
function loadSandbox(tsVersion: string): Promise<SandboxModel> {
  return new Promise((resolve, reject): void => {
    const getLoaderScript = document.createElement('script');
    getLoaderScript.src = 'https://www.typescriptlang.org/js/vs.loader.js';
    getLoaderScript.async = true;
    getLoaderScript.onload = (): void => {
      // For the monaco version you can use unpkg or the TypeScript web infra CDN
      // You can see the available releases for TypeScript here:
      // https://typescript.azureedge.net/indexes/releases.json
      window.require.config({
        paths: {
          linter: '/sandbox',
          sandbox: 'https://www.typescriptlang.org/js/sandbox',
          vs: `https://playgroundcdn.typescriptlang.org/cdn/${tsVersion}/monaco/min/vs`,
        },
        // This is something you need for monaco to work
        ignoreDuplicateModules: ['vs/editor/editor.main'],
      });

      // Grab a copy of monaco, TypeScript and the sandbox
      window.require<[Monaco, Sandbox, WebLinterModule]>(
        ['vs/editor/editor.main', 'sandbox/index', 'linter/index'],
        (main, sandboxFactory, lintUtils) => {
          resolve({ lintUtils, main, sandboxFactory });
        },
        () => {
          reject(
            new Error('Could not get all the dependencies of sandbox set up!'),
          );
        },
      );
    };
    document.body.appendChild(getLoaderScript);
  });
}
```
</details>

- **Parameters**:
  - `tsVersion: string`
- **Return Type**: `Promise<SandboxModel>`
- **Calls**:
  - `document.createElement`
  - `window.require.config`
  - `window.require`
  - `resolve`
  - `reject`
  - `document.body.appendChild`
- **Internal Comments**:
```
// For the monaco version you can use unpkg or the TypeScript web infra CDN (x5)
// You can see the available releases for TypeScript here: (x5)
// https://typescript.azureedge.net/indexes/releases.json (x5)
// This is something you need for monaco to work (x2)
// Grab a copy of monaco, TypeScript and the sandbox (x4)
```

### `sandboxSingleton(version: string): Promise<SandboxModel>`

<details><summary>Code</summary>

```ts
(version: string): Promise<SandboxModel> => {
  if (instance) {
    return instance;
  }
  return (instance = loadSandbox(version));
}
```
</details>

- **Parameters**:
  - `version: string`
- **Return Type**: `Promise<SandboxModel>`
- **Calls**:
  - `loadSandbox`

---

## Interfaces

### `SandboxModel`

<details><summary>Interface Code</summary>

```ts
export interface SandboxModel {
  lintUtils: WebLinterModule;
  main: Monaco;
  sandboxFactory: Sandbox;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `lintUtils` | `WebLinterModule` | ✗ |  |
| `main` | `Monaco` | ✗ |  |
| `sandboxFactory` | `Sandbox` | ✗ |  |


---

## Type Aliases

### `Monaco`

```ts
type Monaco = typeof MonacoEditor;
```

### `Sandbox`

```ts
type Sandbox = typeof SandboxFactory;
```


---