[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `warnAboutTSVersion.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/parseSettings/warnAboutTSVersion.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `semver` | `semver` |
| `ParseSettings` | `./index` |
| `TYPESCRIPT_ESTREE_VERSION` | `../version` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---