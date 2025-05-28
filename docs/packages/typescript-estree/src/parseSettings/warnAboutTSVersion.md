[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `warnAboutTSVersion.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 5 |
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
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/parseSettings/warnAboutTSVersion.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `semver` | `semver` |
| `ParseSettings` | `./index` |
| `TYPESCRIPT_ESTREE_VERSION` | `../version` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `SUPPORTED_TYPESCRIPT_VERSIONS` | `">=4.8.4 <5.9.0"` | const | `'>=4.8.4 <5.9.0'` | ✓ |
| `SUPPORTED_PRERELEASE_RANGES` | `string[]` | const | `[]` | ✗ |
| `ACTIVE_TYPESCRIPT_VERSION` | `any` | const | `ts.version` | ✗ |
| `warnedAboutTSVersion` | `boolean` | let/var | `false` | ✗ |
| `border` | `"============="` | const | `'============='` | ✗ |


---

## Functions

### `warnAboutTSVersion(parseSettings: ParseSettings, passedLoggerFn: boolean): void`

<details><summary>Code</summary>

```ts
export function warnAboutTSVersion(
  parseSettings: ParseSettings,
  passedLoggerFn: boolean,
): void {
  if (isRunningSupportedTypeScriptVersion || warnedAboutTSVersion) {
    return;
  }

  if (
    passedLoggerFn ||
    // See https://github.com/typescript-eslint/typescript-eslint/issues/7896
    // eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
    (typeof process === 'undefined' ? false : process.stdout?.isTTY)
  ) {
    const border = '=============';
    const versionWarning = [
      border,
      '\n',
      'WARNING: You are currently running a version of TypeScript which is not officially supported by @typescript-eslint/typescript-estree.',
      '\n',
      `* @typescript-eslint/typescript-estree version: ${TYPESCRIPT_ESTREE_VERSION}`,
      `* Supported TypeScript versions: ${SUPPORTED_TYPESCRIPT_VERSIONS}`,
      `* Your TypeScript version: ${ACTIVE_TYPESCRIPT_VERSION}`,
      '\n',
      'Please only submit bug reports when using the officially supported version.',
      '\n',
      border,
    ].join('\n');

    parseSettings.log(versionWarning);
  }

  warnedAboutTSVersion = true;
}
```
</details>

- **Parameters**:
  - `parseSettings: ParseSettings`
  - `passedLoggerFn: boolean`
- **Return Type**: `void`
- **Calls**:
  - `[
      border,
      '\n',
      'WARNING: You are currently running a version of TypeScript which is not officially supported by @typescript-eslint/typescript-estree.',
      '\n',
      `* @typescript-eslint/typescript-estree version: ${TYPESCRIPT_ESTREE_VERSION}`,
      `* Supported TypeScript versions: ${SUPPORTED_TYPESCRIPT_VERSIONS}`,
      `* Your TypeScript version: ${ACTIVE_TYPESCRIPT_VERSION}`,
      '\n',
      'Please only submit bug reports when using the officially supported version.',
      '\n',
      border,
    ].join`
  - `parseSettings.log`
- **Internal Comments**:
```
// See https://github.com/typescript-eslint/typescript-eslint/issues/7896
// eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
```


---