[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getParsedConfigFile.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 11
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/tsconfig-utils/src/getParsedConfigFile.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `CORE_COMPILER_OPTIONS` | `./compilerOptions` |


---

## Functions

### `getParsedConfigFile(tsserver: typeof ts, configFile: string, projectDirectory: string): ts.ParsedCommandLine`

<details><summary>Code</summary>

```ts
export function getParsedConfigFile(
  tsserver: typeof ts,
  configFile: string,
  projectDirectory?: string,
): ts.ParsedCommandLine {
  // eslint-disable-next-line @typescript-eslint/no-unnecessary-condition, @typescript-eslint/internal/eqeq-nullish
  if (tsserver.sys === undefined) {
    throw new Error(
      '`getParsedConfigFile` is only supported in a Node-like environment.',
    );
  }

  const parsed = tsserver.getParsedCommandLineOfConfigFile(
    configFile,
    CORE_COMPILER_OPTIONS,
    {
      fileExists: fs.existsSync,
      getCurrentDirectory,
      onUnRecoverableConfigFileDiagnostic: diag => {
        throw new Error(formatDiagnostics([diag])); // ensures that `parsed` is defined.
      },
      readDirectory: tsserver.sys.readDirectory,
      readFile: file =>
        fs.readFileSync(
          path.isAbsolute(file) ? file : path.join(getCurrentDirectory(), file),
          'utf-8',
        ),
      useCaseSensitiveFileNames: tsserver.sys.useCaseSensitiveFileNames,
    },
  );

  if (parsed?.errors.length) {
    throw new Error(formatDiagnostics(parsed.errors));
  }

  // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
  return parsed!;

  function getCurrentDirectory(): string {
    return projectDirectory ? path.resolve(projectDirectory) : process.cwd();
  }

  function formatDiagnostics(diagnostics: ts.Diagnostic[]): string | undefined {
    return tsserver.formatDiagnostics(diagnostics, {
      getCanonicalFileName: f => f,
      getCurrentDirectory,
      getNewLine: () => '\n',
    });
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Parses a TSConfig file using the same logic as tsserver.
 *
 * @param configFile the path to the tsconfig.json file, relative to `projectDirectory`
 * @param projectDirectory the project directory to use as the CWD, defaults to `process.cwd()`
 */
```

- **Parameters**:
  - `tsserver: typeof ts`
  - `configFile: string`
  - `projectDirectory: string`
- **Return Type**: `ts.ParsedCommandLine`
- **Calls**:
  - `tsserver.getParsedCommandLineOfConfigFile`
  - `formatDiagnostics`
  - `fs.readFileSync`
  - `path.isAbsolute`
  - `path.join`
  - `getCurrentDirectory`
  - `path.resolve`
  - `process.cwd`
  - `tsserver.formatDiagnostics`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-unnecessary-condition, @typescript-eslint/internal/eqeq-nullish
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion
```

### `onUnRecoverableConfigFileDiagnostic(diag: any): never`

<details><summary>Code</summary>

```ts
diag => {
        throw new Error(formatDiagnostics([diag])); // ensures that `parsed` is defined.
      }
```
</details>

- **Parameters**:
  - `diag: any`
- **Return Type**: `never`
- **Calls**:
  - `formatDiagnostics`
### `readFile(file: any): any`

<details><summary>Code</summary>

```ts
file =>
        fs.readFileSync(
          path.isAbsolute(file) ? file : path.join(getCurrentDirectory(), file),
          'utf-8',
        )
```
</details>

- **Parameters**:
  - `file: any`
- **Return Type**: `any`
- **Calls**:
  - `fs.readFileSync`
### `onUnRecoverableConfigFileDiagnostic(diag: any): never`

<details><summary>Code</summary>

```ts
diag => {
        throw new Error(formatDiagnostics([diag])); // ensures that `parsed` is defined.
      }
```
</details>

- **Parameters**:
  - `diag: any`
- **Return Type**: `never`
- **Calls**:
  - `formatDiagnostics`
### `readFile(file: any): any`

<details><summary>Code</summary>

```ts
file =>
        fs.readFileSync(
          path.isAbsolute(file) ? file : path.join(getCurrentDirectory(), file),
          'utf-8',
        )
```
</details>

- **Parameters**:
  - `file: any`
- **Return Type**: `any`
- **Calls**:
  - `fs.readFileSync`
### `getCurrentDirectory(): string`

<details><summary>Code</summary>

```ts
function getCurrentDirectory(): string {
    return projectDirectory ? path.resolve(projectDirectory) : process.cwd();
  }
```
</details>

- **Return Type**: `string`
- **Calls**:
  - `path.resolve`
  - `process.cwd`
### `formatDiagnostics(diagnostics: ts.Diagnostic[]): string | undefined`

<details><summary>Code</summary>

```ts
function formatDiagnostics(diagnostics: ts.Diagnostic[]): string | undefined {
    return tsserver.formatDiagnostics(diagnostics, {
      getCanonicalFileName: f => f,
      getCurrentDirectory,
      getNewLine: () => '\n',
    });
  }
```
</details>

- **Parameters**:
  - `diagnostics: ts.Diagnostic[]`
- **Return Type**: `string | undefined`
- **Calls**:
  - `tsserver.formatDiagnostics`
### `getCanonicalFileName(f: any): any`

<details><summary>Code</summary>

```ts
f => f
```
</details>

- **Parameters**:
  - `f: any`
- **Return Type**: `any`
### `getNewLine(): string`

<details><summary>Code</summary>

```ts
() => '\n'
```
</details>

- **Return Type**: `string`
### `getCanonicalFileName(f: any): any`

<details><summary>Code</summary>

```ts
f => f
```
</details>

- **Parameters**:
  - `f: any`
- **Return Type**: `any`
### `getNewLine(): string`

<details><summary>Code</summary>

```ts
() => '\n'
```
</details>

- **Return Type**: `string`

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