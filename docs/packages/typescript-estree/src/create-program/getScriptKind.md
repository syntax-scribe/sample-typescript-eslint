[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getScriptKind.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/create-program/getScriptKind.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `path` | `node:path` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `extension` | `ts.Extension` | const | `path.extname(filePath).toLowerCase() as ts.Extension` | ✗ |


---

## Functions

### `getScriptKind(filePath: string, jsx: boolean): ts.ScriptKind`

<details><summary>Code</summary>

```ts
export function getScriptKind(filePath: string, jsx: boolean): ts.ScriptKind {
  const extension = path.extname(filePath).toLowerCase() as ts.Extension;
  // note - we only respect the user's jsx setting for unknown extensions
  // this is so that we always match TS's internal script kind logic, preventing
  // weird errors due to a mismatch.
  // https://github.com/microsoft/TypeScript/blob/da00ba67ed1182ad334f7c713b8254fba174aeba/src/compiler/utilities.ts#L6948-L6968
  switch (extension) {
    case ts.Extension.Cjs:
    case ts.Extension.Js:
    case ts.Extension.Mjs:
      return ts.ScriptKind.JS;

    case ts.Extension.Cts:
    case ts.Extension.Mts:
    case ts.Extension.Ts:
      return ts.ScriptKind.TS;

    case ts.Extension.Json:
      return ts.ScriptKind.JSON;

    case ts.Extension.Jsx:
      return ts.ScriptKind.JSX;

    case ts.Extension.Tsx:
      return ts.ScriptKind.TSX;

    default:
      // unknown extension, force typescript to ignore the file extension, and respect the user's setting
      return jsx ? ts.ScriptKind.TSX : ts.ScriptKind.TS;
  }
}
```
</details>

- **Parameters**:
  - `filePath: string`
  - `jsx: boolean`
- **Return Type**: `ts.ScriptKind`
- **Calls**:
  - `path.extname(filePath).toLowerCase`
- **Internal Comments**:
```
// note - we only respect the user's jsx setting for unknown extensions
// this is so that we always match TS's internal script kind logic, preventing
// weird errors due to a mismatch.
// https://github.com/microsoft/TypeScript/blob/da00ba67ed1182ad334f7c713b8254fba174aeba/src/compiler/utilities.ts#L6948-L6968
// unknown extension, force typescript to ignore the file extension, and respect the user's setting
```

### `getLanguageVariant(scriptKind: ts.ScriptKind): ts.LanguageVariant`

<details><summary>Code</summary>

```ts
export function getLanguageVariant(
  scriptKind: ts.ScriptKind,
): ts.LanguageVariant {
  // https://github.com/microsoft/TypeScript/blob/d6e483b8dabd8fd37c00954c3f2184bb7f1eb90c/src/compiler/utilities.ts#L6281-L6285
  switch (scriptKind) {
    case ts.ScriptKind.JS:
    case ts.ScriptKind.JSON:
    case ts.ScriptKind.JSX:
    case ts.ScriptKind.TSX:
      return ts.LanguageVariant.JSX;

    default:
      return ts.LanguageVariant.Standard;
  }
}
```
</details>

- **Parameters**:
  - `scriptKind: ts.ScriptKind`
- **Return Type**: `ts.LanguageVariant`
- **Internal Comments**:
```
// https://github.com/microsoft/TypeScript/blob/d6e483b8dabd8fd37c00954c3f2184bb7f1eb90c/src/compiler/utilities.ts#L6281-L6285
```


---