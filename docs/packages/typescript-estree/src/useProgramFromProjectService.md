[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `useProgramFromProjectService.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 9
- **Classes**: 0
- **Imports**: 13
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/useProgramFromProjectService.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ProjectServiceAndMetadata` | `@typescript-eslint/project-service` |
| `debug` | `debug` |
| `minimatch` | `minimatch` |
| `path` | `node:path` |
| `util` | `node:util` |
| `ASTAndDefiniteProgram` | `./create-program/shared` |
| `ASTAndNoProgram` | `./create-program/shared` |
| `ASTAndProgram` | `./create-program/shared` |
| `MutableParseSettings` | `./parseSettings` |
| `createProjectProgram` | `./create-program/createProjectProgram` |
| `createNoProgram` | `./create-program/createSourceFile` |
| `DEFAULT_EXTRA_FILE_EXTENSIONS` | `./create-program/shared` |
| `DEFAULT_PROJECT_FILES_ERROR_EXPLANATION` | `./create-program/validateDefaultProjectForFilesGlob` |


---

## Functions

### `updateExtraFileExtensions(service: ts.server.ProjectService, extraFileExtensions: string[]): void`

<details><summary>Code</summary>

```ts
(
  service: ts.server.ProjectService,
  extraFileExtensions: string[],
): void => {
  const currentServiceFileExtensions = serviceFileExtensions.get(service) ?? [];
  if (
    !util.isDeepStrictEqual(currentServiceFileExtensions, extraFileExtensions)
  ) {
    log(
      'Updating extra file extensions: before=%s: after=%s',
      currentServiceFileExtensions,
      extraFileExtensions,
    );
    service.setHostConfiguration({
      extraFileExtensions: extraFileExtensions.map(extension => ({
        extension,
        isMixedContent: false,
        scriptKind: ts.ScriptKind.Deferred,
      })),
    });
    serviceFileExtensions.set(service, extraFileExtensions);
    log('Extra file extensions updated: %o', extraFileExtensions);
  }
}
```
</details>

- **Parameters**:
  - `service: ts.server.ProjectService`
  - `extraFileExtensions: string[]`
- **Return Type**: `void`
- **Calls**:
  - `serviceFileExtensions.get`
  - `util.isDeepStrictEqual`
  - `log`
  - `service.setHostConfiguration`
  - `extraFileExtensions.map`
  - `serviceFileExtensions.set`
### `openClientFileFromProjectService(defaultProjectMatchedFiles: Set<string>, isDefaultProjectAllowed: boolean, filePathAbsolute: string, parseSettings: Readonly<MutableParseSettings>, serviceAndSettings: ProjectServiceAndMetadata): ts.server.OpenConfiguredProjectResult`

<details><summary>Code</summary>

```ts
function openClientFileFromProjectService(
  defaultProjectMatchedFiles: Set<string>,
  isDefaultProjectAllowed: boolean,
  filePathAbsolute: string,
  parseSettings: Readonly<MutableParseSettings>,
  serviceAndSettings: ProjectServiceAndMetadata,
): ts.server.OpenConfiguredProjectResult {
  const opened = openClientFileAndMaybeReload();

  log('Result from attempting to open client file: %o', opened);

  log(
    'Default project allowed path: %s, based on config file: %s',
    isDefaultProjectAllowed,
    opened.configFileName,
  );

  if (opened.configFileName) {
    if (isDefaultProjectAllowed) {
      throw new Error(
        `${parseSettings.filePath} was included by allowDefaultProject but also was found in the project service. Consider removing it from allowDefaultProject.`,
      );
    }
  } else {
    const wasNotFound = `${parseSettings.filePath} was not found by the project service`;

    const fileExtension = path.extname(parseSettings.filePath);
    const extraFileExtensions = parseSettings.extraFileExtensions;
    if (
      !DEFAULT_EXTRA_FILE_EXTENSIONS.has(fileExtension) &&
      !extraFileExtensions.includes(fileExtension)
    ) {
      const nonStandardExt = `${wasNotFound} because the extension for the file (\`${fileExtension}\`) is non-standard`;
      if (extraFileExtensions.length > 0) {
        throw new Error(
          `${nonStandardExt}. It should be added to your existing \`parserOptions.extraFileExtensions\`.`,
        );
      } else {
        throw new Error(
          `${nonStandardExt}. You should add \`parserOptions.extraFileExtensions\` to your config.`,
        );
      }
    }

    if (!isDefaultProjectAllowed) {
      throw new Error(
        `${wasNotFound}. Consider either including it in the tsconfig.json or including it in allowDefaultProject.`,
      );
    }
  }

  // No a configFileName indicates this file wasn't included in a TSConfig.
  // That means it must get its type information from the default project.
  if (!opened.configFileName) {
    defaultProjectMatchedFiles.add(filePathAbsolute);
    if (
      defaultProjectMatchedFiles.size >
      serviceAndSettings.maximumDefaultProjectFileMatchCount
    ) {
      const filePrintLimit = 20;
      const filesToPrint = [...defaultProjectMatchedFiles].slice(
        0,
        filePrintLimit,
      );
      const truncatedFileCount =
        defaultProjectMatchedFiles.size - filesToPrint.length;

      throw new Error(
        `Too many files (>${serviceAndSettings.maximumDefaultProjectFileMatchCount}) have matched the default project.${DEFAULT_PROJECT_FILES_ERROR_EXPLANATION}
Matching files:
${filesToPrint.map(file => `- ${file}`).join('\n')}
${truncatedFileCount ? `...and ${truncatedFileCount} more files\n` : ''}
If you absolutely need more files included, set parserOptions.projectService.maximumDefaultProjectFileMatchCount_THIS_WILL_SLOW_DOWN_LINTING to a larger value.
`,
      );
    }
  }

  return opened;

  function openClientFile(): ts.server.OpenConfiguredProjectResult {
    return serviceAndSettings.service.openClientFile(
      filePathAbsolute,
      parseSettings.codeFullText,
      /* scriptKind */ undefined,
      parseSettings.tsconfigRootDir,
    );
  }

  function openClientFileAndMaybeReload(): ts.server.OpenConfiguredProjectResult {
    log('Opening project service client file at path: %s', filePathAbsolute);

    let opened = openClientFile();

    // If no project included the file and we're not in single-run mode,
    // we might be running in an editor with outdated file info.
    // We can try refreshing the project service - debounced for performance.
    if (
      !opened.configFileErrors &&
      !opened.configFileName &&
      !parseSettings.singleRun &&
      !isDefaultProjectAllowed &&
      performance.now() - serviceAndSettings.lastReloadTimestamp >
        RELOAD_THROTTLE_MS
    ) {
      log('No config file found; reloading project service and retrying.');
      serviceAndSettings.service.reloadProjects();
      opened = openClientFile();
      serviceAndSettings.lastReloadTimestamp = performance.now();
    }

    return opened;
  }
}
```
</details>

- **Parameters**:
  - `defaultProjectMatchedFiles: Set<string>`
  - `isDefaultProjectAllowed: boolean`
  - `filePathAbsolute: string`
  - `parseSettings: Readonly<MutableParseSettings>`
  - `serviceAndSettings: ProjectServiceAndMetadata`
- **Return Type**: `ts.server.OpenConfiguredProjectResult`
- **Calls**:
  - `openClientFileAndMaybeReload`
  - `log`
  - `path.extname`
  - `DEFAULT_EXTRA_FILE_EXTENSIONS.has`
  - `extraFileExtensions.includes`
  - `defaultProjectMatchedFiles.add`
  - `[...defaultProjectMatchedFiles].slice`
  - `filesToPrint.map(file => `- ${file}`).join`
  - `serviceAndSettings.service.openClientFile`
  - `openClientFile`
  - `performance.now`
  - `serviceAndSettings.service.reloadProjects`
- **Internal Comments**:
```
// No a configFileName indicates this file wasn't included in a TSConfig.
// That means it must get its type information from the default project.
/* scriptKind */
// If no project included the file and we're not in single-run mode,
// we might be running in an editor with outdated file info.
// We can try refreshing the project service - debounced for performance.
```

### `openClientFile(): ts.server.OpenConfiguredProjectResult`

<details><summary>Code</summary>

```ts
function openClientFile(): ts.server.OpenConfiguredProjectResult {
    return serviceAndSettings.service.openClientFile(
      filePathAbsolute,
      parseSettings.codeFullText,
      /* scriptKind */ undefined,
      parseSettings.tsconfigRootDir,
    );
  }
```
</details>

- **Return Type**: `ts.server.OpenConfiguredProjectResult`
- **Calls**:
  - `serviceAndSettings.service.openClientFile`
- **Internal Comments**:
```
/* scriptKind */
```

### `openClientFileAndMaybeReload(): ts.server.OpenConfiguredProjectResult`

<details><summary>Code</summary>

```ts
function openClientFileAndMaybeReload(): ts.server.OpenConfiguredProjectResult {
    log('Opening project service client file at path: %s', filePathAbsolute);

    let opened = openClientFile();

    // If no project included the file and we're not in single-run mode,
    // we might be running in an editor with outdated file info.
    // We can try refreshing the project service - debounced for performance.
    if (
      !opened.configFileErrors &&
      !opened.configFileName &&
      !parseSettings.singleRun &&
      !isDefaultProjectAllowed &&
      performance.now() - serviceAndSettings.lastReloadTimestamp >
        RELOAD_THROTTLE_MS
    ) {
      log('No config file found; reloading project service and retrying.');
      serviceAndSettings.service.reloadProjects();
      opened = openClientFile();
      serviceAndSettings.lastReloadTimestamp = performance.now();
    }

    return opened;
  }
```
</details>

- **Return Type**: `ts.server.OpenConfiguredProjectResult`
- **Calls**:
  - `log`
  - `openClientFile`
  - `performance.now`
  - `serviceAndSettings.service.reloadProjects`
- **Internal Comments**:
```
// If no project included the file and we're not in single-run mode,
// we might be running in an editor with outdated file info.
// We can try refreshing the project service - debounced for performance.
```

### `createNoProgramWithProjectService(filePathAbsolute: string, parseSettings: Readonly<MutableParseSettings>, service: ts.server.ProjectService): ASTAndNoProgram`

<details><summary>Code</summary>

```ts
function createNoProgramWithProjectService(
  filePathAbsolute: string,
  parseSettings: Readonly<MutableParseSettings>,
  service: ts.server.ProjectService,
): ASTAndNoProgram {
  log('No project service information available. Creating no program.');

  // If the project service knows about this file, this informs if of changes.
  // Doing so ensures that:
  // - if the file is not part of a project, we don't waste time creating a program (fast non-type-aware linting)
  // - otherwise, we refresh the file in the project service (moderately fast, since the project is already loaded)
  if (service.getScriptInfo(filePathAbsolute)) {
    log('Script info available. Opening client file in project service.');
    service.openClientFile(
      filePathAbsolute,
      parseSettings.codeFullText,
      /* scriptKind */ undefined,
      parseSettings.tsconfigRootDir,
    );
  }

  return createNoProgram(parseSettings);
}
```
</details>

- **Parameters**:
  - `filePathAbsolute: string`
  - `parseSettings: Readonly<MutableParseSettings>`
  - `service: ts.server.ProjectService`
- **Return Type**: `ASTAndNoProgram`
- **Calls**:
  - `log`
  - `service.getScriptInfo`
  - `service.openClientFile`
  - `createNoProgram (from ./create-program/createSourceFile)`
- **Internal Comments**:
```
// If the project service knows about this file, this informs if of changes.
// Doing so ensures that:
// - if the file is not part of a project, we don't waste time creating a program (fast non-type-aware linting)
// - otherwise, we refresh the file in the project service (moderately fast, since the project is already loaded)
/* scriptKind */
```

### `retrieveASTAndProgramFor(filePathAbsolute: string, parseSettings: Readonly<MutableParseSettings>, serviceAndSettings: ProjectServiceAndMetadata): ASTAndDefiniteProgram | undefined`

<details><summary>Code</summary>

```ts
function retrieveASTAndProgramFor(
  filePathAbsolute: string,
  parseSettings: Readonly<MutableParseSettings>,
  serviceAndSettings: ProjectServiceAndMetadata,
): ASTAndDefiniteProgram | undefined {
  log('Retrieving script info and then program for: %s', filePathAbsolute);

  const scriptInfo = serviceAndSettings.service.getScriptInfo(filePathAbsolute);
  /* eslint-disable @typescript-eslint/no-non-null-assertion */
  const program = serviceAndSettings.service
    .getDefaultProjectForFile(scriptInfo!.fileName, true)!
    .getLanguageService(/*ensureSynchronized*/ true)
    .getProgram();
  /* eslint-enable @typescript-eslint/no-non-null-assertion */

  if (!program) {
    log('Could not find project service program for: %s', filePathAbsolute);
    return undefined;
  }

  log('Found project service program for: %s', filePathAbsolute);

  return createProjectProgram(parseSettings, [program]);
}
```
</details>

- **Parameters**:
  - `filePathAbsolute: string`
  - `parseSettings: Readonly<MutableParseSettings>`
  - `serviceAndSettings: ProjectServiceAndMetadata`
- **Return Type**: `ASTAndDefiniteProgram | undefined`
- **Calls**:
  - `log`
  - `serviceAndSettings.service.getScriptInfo`
  - `serviceAndSettings.service
    .getDefaultProjectForFile(scriptInfo!.fileName, true)!
    .getLanguageService(/*ensureSynchronized*/ true)
    .getProgram`
  - `createProjectProgram (from ./create-program/createProjectProgram)`
- **Internal Comments**:
```
/* eslint-disable @typescript-eslint/no-non-null-assertion */ (x2)
/* eslint-enable @typescript-eslint/no-non-null-assertion */
```

### `useProgramFromProjectService(serviceAndSettings: ProjectServiceAndMetadata, parseSettings: Readonly<MutableParseSettings>, hasFullTypeInformation: boolean, defaultProjectMatchedFiles: Set<string>): ASTAndProgram | undefined`

<details><summary>Code</summary>

```ts
export function useProgramFromProjectService(
  serviceAndSettings: ProjectServiceAndMetadata,
  parseSettings: Readonly<MutableParseSettings>,
  hasFullTypeInformation: boolean,
  defaultProjectMatchedFiles: Set<string>,
): ASTAndProgram | undefined;
```
</details>

- **Parameters**:
  - `serviceAndSettings: ProjectServiceAndMetadata`
  - `parseSettings: Readonly<MutableParseSettings>`
  - `hasFullTypeInformation: boolean`
  - `defaultProjectMatchedFiles: Set<string>`
- **Return Type**: `ASTAndProgram | undefined`
### `absolutify(filePath: string, serviceAndSettings: ProjectServiceAndMetadata): string`

<details><summary>Code</summary>

```ts
function absolutify(
  filePath: string,
  serviceAndSettings: ProjectServiceAndMetadata,
): string {
  return path.isAbsolute(filePath)
    ? filePath
    : path.join(
        serviceAndSettings.service.host.getCurrentDirectory(),
        filePath,
      );
}
```
</details>

- **Parameters**:
  - `filePath: string`
  - `serviceAndSettings: ProjectServiceAndMetadata`
- **Return Type**: `string`
- **Calls**:
  - `path.isAbsolute`
  - `path.join`
  - `serviceAndSettings.service.host.getCurrentDirectory`
### `filePathMatchedBy(filePath: string, allowDefaultProject: string[] | undefined): boolean`

<details><summary>Code</summary>

```ts
function filePathMatchedBy(
  filePath: string,
  allowDefaultProject: string[] | undefined,
): boolean {
  return !!allowDefaultProject?.some(pattern => minimatch(filePath, pattern));
}
```
</details>

- **Parameters**:
  - `filePath: string`
  - `allowDefaultProject: string[] | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `allowDefaultProject?.some`
  - `minimatch (from minimatch)`

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