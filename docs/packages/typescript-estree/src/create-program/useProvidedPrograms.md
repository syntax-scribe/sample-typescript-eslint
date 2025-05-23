[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useProvidedPrograms.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/create-program/useProvidedPrograms.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `getParsedConfigFile` | `@typescript-eslint/tsconfig-utils` |
| `debug` | `debug` |
| `ParseSettings` | `../parseSettings` |
| `ASTAndDefiniteProgram` | `./shared` |
| `getAstFromProgram` | `./shared` |


---

## Functions

### `useProvidedPrograms(programInstances: Iterable<ts.Program>, parseSettings: ParseSettings): ASTAndDefiniteProgram | undefined`

<details><summary>Code</summary>

```ts
export function useProvidedPrograms(
  programInstances: Iterable<ts.Program>,
  parseSettings: ParseSettings,
): ASTAndDefiniteProgram | undefined {
  log(
    'Retrieving ast for %s from provided program instance(s)',
    parseSettings.filePath,
  );

  let astAndProgram: ASTAndDefiniteProgram | undefined;
  for (const programInstance of programInstances) {
    astAndProgram = getAstFromProgram(programInstance, parseSettings.filePath);
    // Stop at the first applicable program instance
    if (astAndProgram) {
      break;
    }
  }

  if (astAndProgram) {
    astAndProgram.program.getTypeChecker(); // ensure parent pointers are set in source files
    return astAndProgram;
  }

  const relativeFilePath = path.relative(
    parseSettings.tsconfigRootDir,
    parseSettings.filePath,
  );

  const [typeSource, typeSources] =
    parseSettings.projects.size > 0
      ? ['project', 'project(s)']
      : ['programs', 'program instance(s)'];

  const errorLines = [
    `"parserOptions.${typeSource}" has been provided for @typescript-eslint/parser.`,
    `The file was not found in any of the provided ${typeSources}: ${relativeFilePath}`,
  ];

  throw new Error(errorLines.join('\n'));
}
```
</details>

- **Parameters**:
  - `programInstances: Iterable<ts.Program>`
  - `parseSettings: ParseSettings`
- **Return Type**: `ASTAndDefiniteProgram | undefined`
- **Calls**:
  - `log`
  - `getAstFromProgram (from ./shared)`
  - `astAndProgram.program.getTypeChecker`
  - `path.relative`
  - `errorLines.join`
- **Internal Comments**:
```
// Stop at the first applicable program instance
```

### `createProgramFromConfigFile(configFile: string, projectDirectory: string): ts.Program`

<details><summary>Code</summary>

```ts
export function createProgramFromConfigFile(
  configFile: string,
  projectDirectory?: string,
): ts.Program {
  const parsed = getParsedConfigFile(ts, configFile, projectDirectory);
  const host = ts.createCompilerHost(parsed.options, true);
  return ts.createProgram(parsed.fileNames, parsed.options, host);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Utility offered by parser to help consumers construct their own program instance.
 *
 * @param configFile the path to the tsconfig.json file, relative to `projectDirectory`
 * @param projectDirectory the project directory to use as the CWD, defaults to `process.cwd()`
 */
```

- **Parameters**:
  - `configFile: string`
  - `projectDirectory: string`
- **Return Type**: `ts.Program`
- **Calls**:
  - `getParsedConfigFile (from @typescript-eslint/tsconfig-utils)`
  - `ts.createCompilerHost`
  - `ts.createProgram`

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