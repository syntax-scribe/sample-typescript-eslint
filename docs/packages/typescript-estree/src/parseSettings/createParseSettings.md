[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `createParseSettings.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 📦 Imports | 17 |
| 📊 Variables & Constants | 9 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/parseSettings/createParseSettings.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `CreateProjectServiceSettings` | `@typescript-eslint/project-service` |
| `ProjectServiceAndMetadata` | `@typescript-eslint/project-service` |
| `ProjectServiceOptions` | `@typescript-eslint/types` |
| `createProjectService` | `@typescript-eslint/project-service` |
| `debug` | `debug` |
| `path` | `node:path` |
| `TSESTreeOptions` | `../parser-options` |
| `MutableParseSettings` | `./index` |
| `ensureAbsolutePath` | `../create-program/shared` |
| `validateDefaultProjectForFilesGlob` | `../create-program/validateDefaultProjectForFilesGlob` |
| `isSourceFile` | `../source-files` |
| `DEFAULT_TSCONFIG_CACHE_DURATION_SECONDS` | `./ExpiringCache` |
| `ExpiringCache` | `./ExpiringCache` |
| `getProjectConfigFiles` | `./getProjectConfigFiles` |
| `inferSingleRun` | `./inferSingleRun` |
| `resolveProjectList` | `./resolveProjectList` |
| `warnAboutTSVersion` | `./warnAboutTSVersion` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `TSCONFIG_MATCH_CACHE` | `ExpiringCache<string, string> | null` | let/var | `*not shown*` | ✗ |
| `TSSERVER_PROJECT_SERVICE` | `ProjectServiceAndMetadata | null` | let/var | `null` | ✗ |
| `JSDocParsingMode` | `{ readonly ParseAll: any; readonly ParseForTypeErrors: any; readonly ParseForTypeInfo: any; readonly ParseNone: any; }` | const | `{
  ParseAll: ts.JSDocParsingMode?.ParseAll,
  ParseForTypeErrors: ts.JSDocParsingMode?.ParseForTypeErrors,
  ParseForTypeInfo: ts.JSDocParsingMode?.ParseForTypeInfo,
  ParseNone: ts.JSDocParsingMode?.ParseNone,
} as const` | ✗ |
| `tsconfigRootDir` | `string` | const | `typeof tsestreeOptions.tsconfigRootDir === 'string'
      ? tsestreeOptions.tsconfigRootDir
      : process.cwd()` | ✗ |
| `passedLoggerFn` | `boolean` | const | `typeof tsestreeOptions.loggerFn === 'function'` | ✗ |
| `extension` | `ts.Extension` | const | `path.extname(filePath).toLowerCase() as ts.Extension` | ✗ |
| `parseSettings` | `MutableParseSettings` | const | `{
    loc: tsestreeOptions.loc === true,
    range: tsestreeOptions.range === true,
    allowInvalidAST: tsestreeOptions.allowInvalidAST === true,
    code,
    codeFullText,
    comment: tsestreeOptions.comment === true,
    comments: [],
    debugLevel:
      tsestreeOptions.debugLevel === true
        ? new Set(['typescript-eslint'])
        : Array.isArray(tsestreeOptions.debugLevel)
          ? new Set(tsestreeOptions.debugLevel)
          : new Set(),
    errorOnTypeScriptSyntacticAndSemanticIssues: false,
    errorOnUnknownASTType: tsestreeOptions.errorOnUnknownASTType === true,
    extraFileExtensions:
      Array.isArray(tsestreeOptions.extraFileExtensions) &&
      tsestreeOptions.extraFileExtensions.every(ext => typeof ext === 'string')
        ? tsestreeOptions.extraFileExtensions
        : [],
    filePath,
    jsDocParsingMode,
    jsx: tsestreeOptions.jsx === true,
    log:
      typeof tsestreeOptions.loggerFn === 'function'
        ? tsestreeOptions.loggerFn
        : tsestreeOptions.loggerFn === false
          ? (): void => {} // eslint-disable-line @typescript-eslint/no-empty-function
          : console.log, // eslint-disable-line no-console
    preserveNodeMaps: tsestreeOptions.preserveNodeMaps !== false,
    programs: Array.isArray(tsestreeOptions.programs)
      ? tsestreeOptions.programs
      : null,
    projects: new Map(),
    projectService:
      tsestreeOptions.projectService ||
      (tsestreeOptions.project &&
        tsestreeOptions.projectService !== false &&
        process.env.TYPESCRIPT_ESLINT_PROJECT_SERVICE === 'true')
        ? populateProjectService(tsestreeOptions.projectService, {
            jsDocParsingMode,
            tsconfigRootDir,
          })
        : undefined,
    setExternalModuleIndicator:
      tsestreeOptions.sourceType === 'module' ||
      (tsestreeOptions.sourceType == null && extension === ts.Extension.Mjs) ||
      (tsestreeOptions.sourceType == null && extension === ts.Extension.Mts)
        ? (file): void => {
            file.externalModuleIndicator = true;
          }
        : undefined,
    singleRun,
    suppressDeprecatedPropertyWarnings:
      tsestreeOptions.suppressDeprecatedPropertyWarnings ??
      process.env.NODE_ENV !== 'test',
    tokens: tsestreeOptions.tokens === true ? [] : null,
    tsconfigMatchCache: (TSCONFIG_MATCH_CACHE ??= new ExpiringCache(
      singleRun
        ? 'Infinity'
        : (tsestreeOptions.cacheLifetime?.glob ??
          DEFAULT_TSCONFIG_CACHE_DURATION_SECONDS),
    )),
    tsconfigRootDir,
  }` | ✗ |
| `namespaces` | `any[]` | const | `[]` | ✗ |
| `options` | `any` | const | `typeof optionsRaw === 'object' ? optionsRaw : {}` | ✗ |


---

## Functions

### `createParseSettings(code: string | ts.SourceFile, tsestreeOptions: Partial<TSESTreeOptions>): MutableParseSettings`

<details><summary>Code</summary>

```ts
export function createParseSettings(
  code: string | ts.SourceFile,
  tsestreeOptions: Partial<TSESTreeOptions> = {},
): MutableParseSettings {
  const codeFullText = enforceCodeString(code);
  const singleRun = inferSingleRun(tsestreeOptions);
  const tsconfigRootDir =
    typeof tsestreeOptions.tsconfigRootDir === 'string'
      ? tsestreeOptions.tsconfigRootDir
      : process.cwd();
  const passedLoggerFn = typeof tsestreeOptions.loggerFn === 'function';
  const filePath = ensureAbsolutePath(
    typeof tsestreeOptions.filePath === 'string' &&
      tsestreeOptions.filePath !== '<input>'
      ? tsestreeOptions.filePath
      : getFileName(tsestreeOptions.jsx),
    tsconfigRootDir,
  );
  const extension = path.extname(filePath).toLowerCase() as ts.Extension;
  const jsDocParsingMode = ((): ts.JSDocParsingMode => {
    switch (tsestreeOptions.jsDocParsingMode) {
      case 'all':
        return JSDocParsingMode.ParseAll;

      case 'none':
        return JSDocParsingMode.ParseNone;

      case 'type-info':
        return JSDocParsingMode.ParseForTypeInfo;

      default:
        return JSDocParsingMode.ParseAll;
    }
  })();

  const parseSettings: MutableParseSettings = {
    loc: tsestreeOptions.loc === true,
    range: tsestreeOptions.range === true,
    allowInvalidAST: tsestreeOptions.allowInvalidAST === true,
    code,
    codeFullText,
    comment: tsestreeOptions.comment === true,
    comments: [],
    debugLevel:
      tsestreeOptions.debugLevel === true
        ? new Set(['typescript-eslint'])
        : Array.isArray(tsestreeOptions.debugLevel)
          ? new Set(tsestreeOptions.debugLevel)
          : new Set(),
    errorOnTypeScriptSyntacticAndSemanticIssues: false,
    errorOnUnknownASTType: tsestreeOptions.errorOnUnknownASTType === true,
    extraFileExtensions:
      Array.isArray(tsestreeOptions.extraFileExtensions) &&
      tsestreeOptions.extraFileExtensions.every(ext => typeof ext === 'string')
        ? tsestreeOptions.extraFileExtensions
        : [],
    filePath,
    jsDocParsingMode,
    jsx: tsestreeOptions.jsx === true,
    log:
      typeof tsestreeOptions.loggerFn === 'function'
        ? tsestreeOptions.loggerFn
        : tsestreeOptions.loggerFn === false
          ? (): void => {} // eslint-disable-line @typescript-eslint/no-empty-function
          : console.log, // eslint-disable-line no-console
    preserveNodeMaps: tsestreeOptions.preserveNodeMaps !== false,
    programs: Array.isArray(tsestreeOptions.programs)
      ? tsestreeOptions.programs
      : null,
    projects: new Map(),
    projectService:
      tsestreeOptions.projectService ||
      (tsestreeOptions.project &&
        tsestreeOptions.projectService !== false &&
        process.env.TYPESCRIPT_ESLINT_PROJECT_SERVICE === 'true')
        ? populateProjectService(tsestreeOptions.projectService, {
            jsDocParsingMode,
            tsconfigRootDir,
          })
        : undefined,
    setExternalModuleIndicator:
      tsestreeOptions.sourceType === 'module' ||
      (tsestreeOptions.sourceType == null && extension === ts.Extension.Mjs) ||
      (tsestreeOptions.sourceType == null && extension === ts.Extension.Mts)
        ? (file): void => {
            file.externalModuleIndicator = true;
          }
        : undefined,
    singleRun,
    suppressDeprecatedPropertyWarnings:
      tsestreeOptions.suppressDeprecatedPropertyWarnings ??
      process.env.NODE_ENV !== 'test',
    tokens: tsestreeOptions.tokens === true ? [] : null,
    tsconfigMatchCache: (TSCONFIG_MATCH_CACHE ??= new ExpiringCache(
      singleRun
        ? 'Infinity'
        : (tsestreeOptions.cacheLifetime?.glob ??
          DEFAULT_TSCONFIG_CACHE_DURATION_SECONDS),
    )),
    tsconfigRootDir,
  };

  // debug doesn't support multiple `enable` calls, so have to do it all at once
  if (parseSettings.debugLevel.size > 0) {
    const namespaces = [];
    if (parseSettings.debugLevel.has('typescript-eslint')) {
      namespaces.push('typescript-eslint:*');
    }
    if (
      parseSettings.debugLevel.has('eslint') ||
      // make sure we don't turn off the eslint debug if it was enabled via --debug
      debug.enabled('eslint:*,-eslint:code-path')
    ) {
      // https://github.com/eslint/eslint/blob/9dfc8501fb1956c90dc11e6377b4cb38a6bea65d/bin/eslint.js#L25
      namespaces.push('eslint:*,-eslint:code-path');
    }
    debug.enable(namespaces.join(','));
  }

  if (Array.isArray(tsestreeOptions.programs)) {
    if (!tsestreeOptions.programs.length) {
      throw new Error(
        `You have set parserOptions.programs to an empty array. This will cause all files to not be found in existing programs. Either provide one or more existing TypeScript Program instances in the array, or remove the parserOptions.programs setting.`,
      );
    }
    log(
      'parserOptions.programs was provided, so parserOptions.project will be ignored.',
    );
  }

  // Providing a program or project service overrides project resolution
  if (!parseSettings.programs && !parseSettings.projectService) {
    parseSettings.projects = resolveProjectList({
      cacheLifetime: tsestreeOptions.cacheLifetime,
      project: getProjectConfigFiles(parseSettings, tsestreeOptions.project),
      projectFolderIgnoreList: tsestreeOptions.projectFolderIgnoreList,
      singleRun: parseSettings.singleRun,
      tsconfigRootDir,
    });
  }

  // No type-aware linting which means that cross-file (or even same-file) JSDoc is useless
  // So in this specific case we default to 'none' if no value was provided
  if (
    tsestreeOptions.jsDocParsingMode == null &&
    parseSettings.projects.size === 0 &&
    parseSettings.programs == null &&
    parseSettings.projectService == null
  ) {
    parseSettings.jsDocParsingMode = JSDocParsingMode.ParseNone;
  }

  warnAboutTSVersion(parseSettings, passedLoggerFn);

  return parseSettings;
}
```
</details>

- **Parameters**:
  - `code: string | ts.SourceFile`
  - `tsestreeOptions: Partial<TSESTreeOptions>`
- **Return Type**: `MutableParseSettings`
- **Calls**:
  - `enforceCodeString`
  - `inferSingleRun (from ./inferSingleRun)`
  - `process.cwd`
  - `ensureAbsolutePath (from ../create-program/shared)`
  - `getFileName`
  - `path.extname(filePath).toLowerCase`
  - `complex_call_2699`
  - `Array.isArray`
  - `tsestreeOptions.extraFileExtensions.every`
  - `populateProjectService`
  - `parseSettings.debugLevel.has`
  - `namespaces.push`
  - `debug.enabled`
  - `debug.enable`
  - `namespaces.join`
  - `log`
  - `resolveProjectList (from ./resolveProjectList)`
  - `getProjectConfigFiles (from ./getProjectConfigFiles)`
  - `warnAboutTSVersion (from ./warnAboutTSVersion)`
- **Internal Comments**:
```
// debug doesn't support multiple `enable` calls, so have to do it all at once
// make sure we don't turn off the eslint debug if it was enabled via --debug (x3)
// https://github.com/eslint/eslint/blob/9dfc8501fb1956c90dc11e6377b4cb38a6bea65d/bin/eslint.js#L25 (x4)
// Providing a program or project service overrides project resolution
// No type-aware linting which means that cross-file (or even same-file) JSDoc is useless
// So in this specific case we default to 'none' if no value was provided
```

### `clearTSConfigMatchCache(): void`

<details><summary>Code</summary>

```ts
export function clearTSConfigMatchCache(): void {
  TSCONFIG_MATCH_CACHE?.clear();
}
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `TSCONFIG_MATCH_CACHE?.clear`
### `clearTSServerProjectService(): void`

<details><summary>Code</summary>

```ts
export function clearTSServerProjectService(): void {
  TSSERVER_PROJECT_SERVICE = null;
}
```
</details>

- **Return Type**: `void`
### `enforceCodeString(code: unknown): string`

<details><summary>Code</summary>

```ts
function enforceCodeString(code: unknown): string {
  return isSourceFile(code)
    ? code.getFullText(code)
    : typeof code === 'string'
      ? code
      : String(code);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Ensures source code is a string.
 */
```

- **Parameters**:
  - `code: unknown`
- **Return Type**: `string`
- **Calls**:
  - `isSourceFile (from ../source-files)`
  - `code.getFullText`
  - `String`
### `getFileName(jsx: boolean): string`

<details><summary>Code</summary>

```ts
function getFileName(jsx?: boolean): string {
  return jsx ? 'estree.tsx' : 'estree.ts';
}
```
</details>

- **JSDoc**:
```ts
/**
 * Compute the filename based on the parser options.
 *
 * Even if jsx option is set in typescript compiler, filename still has to
 * contain .tsx file extension.
 */
```

- **Parameters**:
  - `jsx: boolean`
- **Return Type**: `string`
### `populateProjectService(optionsRaw: ProjectServiceOptions | true | undefined, settings: CreateProjectServiceSettings): any`

<details><summary>Code</summary>

```ts
function populateProjectService(
  optionsRaw: ProjectServiceOptions | true | undefined,
  settings: CreateProjectServiceSettings,
) {
  const options = typeof optionsRaw === 'object' ? optionsRaw : {};

  validateDefaultProjectForFilesGlob(options.allowDefaultProject);

  TSSERVER_PROJECT_SERVICE ??= createProjectService({
    options,
    ...settings,
  });

  return TSSERVER_PROJECT_SERVICE;
}
```
</details>

- **Parameters**:
  - `optionsRaw: ProjectServiceOptions | true | undefined`
  - `settings: CreateProjectServiceSettings`
- **Return Type**: `any`
- **Calls**:
  - `validateDefaultProjectForFilesGlob (from ../create-program/validateDefaultProjectForFilesGlob)`
  - `createProjectService (from @typescript-eslint/project-service)`

---