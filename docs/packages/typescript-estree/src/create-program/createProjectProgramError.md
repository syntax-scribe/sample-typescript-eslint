[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `createProjectProgramError.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/create-program/createProjectProgramError.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `path` | `node:path` |
| `ParseSettings` | `../parseSettings` |
| `describeFilePath` | `./describeFilePath` |
| `DEFAULT_EXTRA_FILE_EXTENSIONS` | `./shared` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `describedPrograms` | `string` | const | `relativeProjects.length === 1
      ? ` ${relativeProjects[0]}`
      : `\n${relativeProjects.map(project => `- ${project}`).join('\n')}`` | ✗ |
| `details` | `string[]` | const | `[]` | ✗ |
| `nonStandardExt` | `string` | const | ``The extension for the file (\`${fileExtension}\`) is non-standard`` | ✗ |


---

## Functions

### `createProjectProgramError(parseSettings: ParseSettings, programsForProjects: readonly ts.Program[]): string[]`

<details><summary>Code</summary>

```ts
export function createProjectProgramError(
  parseSettings: ParseSettings,
  programsForProjects: readonly ts.Program[],
): string[] {
  const describedFilePath = describeFilePath(
    parseSettings.filePath,
    parseSettings.tsconfigRootDir,
  );

  return [
    getErrorStart(describedFilePath, parseSettings),
    ...getErrorDetails(describedFilePath, parseSettings, programsForProjects),
  ];
}
```
</details>

- **Parameters**:
  - `parseSettings: ParseSettings`
  - `programsForProjects: readonly ts.Program[]`
- **Return Type**: `string[]`
- **Calls**:
  - `describeFilePath (from ./describeFilePath)`
  - `getErrorStart`
  - `getErrorDetails`
### `getErrorStart(describedFilePath: string, parseSettings: ParseSettings): string`

<details><summary>Code</summary>

```ts
function getErrorStart(
  describedFilePath: string,
  parseSettings: ParseSettings,
): string {
  const relativeProjects = [...parseSettings.projects.values()].map(
    projectFile => describeFilePath(projectFile, parseSettings.tsconfigRootDir),
  );

  const describedPrograms =
    relativeProjects.length === 1
      ? ` ${relativeProjects[0]}`
      : `\n${relativeProjects.map(project => `- ${project}`).join('\n')}`;

  return `ESLint was configured to run on \`${describedFilePath}\` using \`parserOptions.project\`:${describedPrograms}`;
}
```
</details>

- **Parameters**:
  - `describedFilePath: string`
  - `parseSettings: ParseSettings`
- **Return Type**: `string`
- **Calls**:
  - `[...parseSettings.projects.values()].map`
  - `parseSettings.projects.values`
  - `describeFilePath (from ./describeFilePath)`
  - `relativeProjects.map(project => `- ${project}`).join`
### `getErrorDetails(describedFilePath: string, parseSettings: ParseSettings, programsForProjects: readonly ts.Program[]): string[]`

<details><summary>Code</summary>

```ts
function getErrorDetails(
  describedFilePath: string,
  parseSettings: ParseSettings,
  programsForProjects: readonly ts.Program[],
): string[] {
  if (
    programsForProjects.length === 1 &&
    programsForProjects[0].getProjectReferences()?.length
  ) {
    return [
      `That TSConfig uses project "references" and doesn't include \`${describedFilePath}\` directly, which is not supported by \`parserOptions.project\`.`,
      `Either:`,
      `- Switch to \`parserOptions.projectService\``,
      `- Use an ESLint-specific TSConfig`,
      `See the typescript-eslint docs for more info: https://typescript-eslint.io/troubleshooting/typed-linting#are-typescript-project-references-supported`,
    ];
  }

  const { extraFileExtensions } = parseSettings;
  const details: string[] = [];

  for (const extraExtension of extraFileExtensions) {
    if (!extraExtension.startsWith('.')) {
      details.push(
        `Found unexpected extension \`${extraExtension}\` specified with the \`parserOptions.extraFileExtensions\` option. Did you mean \`.${extraExtension}\`?`,
      );
    }
    if (DEFAULT_EXTRA_FILE_EXTENSIONS.has(extraExtension)) {
      details.push(
        `You unnecessarily included the extension \`${extraExtension}\` with the \`parserOptions.extraFileExtensions\` option. This extension is already handled by the parser by default.`,
      );
    }
  }

  const fileExtension = path.extname(parseSettings.filePath);
  if (!DEFAULT_EXTRA_FILE_EXTENSIONS.has(fileExtension)) {
    const nonStandardExt = `The extension for the file (\`${fileExtension}\`) is non-standard`;
    if (extraFileExtensions.length > 0) {
      if (!extraFileExtensions.includes(fileExtension)) {
        return [
          ...details,
          `${nonStandardExt}. It should be added to your existing \`parserOptions.extraFileExtensions\`.`,
        ];
      }
    } else {
      return [
        ...details,
        `${nonStandardExt}. You should add \`parserOptions.extraFileExtensions\` to your config.`,
      ];
    }
  }

  const [describedInclusions, describedSpecifiers] =
    parseSettings.projects.size === 1
      ? ['that TSConfig does not', 'that TSConfig']
      : ['none of those TSConfigs', 'one of those TSConfigs'];

  return [
    ...details,
    `However, ${describedInclusions} include this file. Either:`,
    `- Change ESLint's list of included files to not include this file`,
    `- Change ${describedSpecifiers} to include this file`,
    `- Create a new TSConfig that includes this file and include it in your parserOptions.project`,
    `See the typescript-eslint docs for more info: https://typescript-eslint.io/troubleshooting/typed-linting#i-get-errors-telling-me-eslint-was-configured-to-run--however-that-tsconfig-does-not--none-of-those-tsconfigs-include-this-file`,
  ];
}
```
</details>

- **Parameters**:
  - `describedFilePath: string`
  - `parseSettings: ParseSettings`
  - `programsForProjects: readonly ts.Program[]`
- **Return Type**: `string[]`
- **Calls**:
  - `programsForProjects[0].getProjectReferences`
  - `extraExtension.startsWith`
  - `details.push`
  - `DEFAULT_EXTRA_FILE_EXTENSIONS.has`
  - `path.extname`
  - `extraFileExtensions.includes`

---