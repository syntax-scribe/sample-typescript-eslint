[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `parser.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 7
- **Classes**: 0
- **Imports**: 21
- **Interfaces**: 2
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/parser.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `debug` | `debug` |
| `ASTAndProgram` | `./create-program/shared` |
| `CanonicalPath` | `./create-program/shared` |
| `ParserServices` | `./parser-options` |
| `ParserServicesNodeMaps` | `./parser-options` |
| `TSESTreeOptions` | `./parser-options` |
| `ParseSettings` | `./parseSettings` |
| `TSESTree` | `./ts-estree` |
| `astConverter` | `./ast-converter` |
| `convertError` | `./convert` |
| `createIsolatedProgram` | `./create-program/createIsolatedProgram` |
| `createProjectProgram` | `./create-program/createProjectProgram` |
| `createNoProgram` | `./create-program/createSourceFile` |
| `createSourceFile` | `./create-program/createSourceFile` |
| `getWatchProgramsForProjects` | `./create-program/getWatchProgramsForProjects` |
| `createProgramFromConfigFile` | `./create-program/useProvidedPrograms` |
| `useProvidedPrograms` | `./create-program/useProvidedPrograms` |
| `createParserServices` | `./createParserServices` |
| `createParseSettings` | `./parseSettings/createParseSettings` |
| `getFirstSemanticOrSyntacticError` | `./semantic-or-syntactic-errors` |
| `useProgramFromProjectService` | `./useProgramFromProjectService` |


---

## Functions

### `clearProgramCache(): void`

<details><summary>Code</summary>

```ts
export function clearProgramCache(): void {
  existingPrograms.clear();
}
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `existingPrograms.clear`
### `clearDefaultProjectMatchedFiles(): void`

<details><summary>Code</summary>

```ts
export function clearDefaultProjectMatchedFiles(): void {
  defaultProjectMatchedFiles.clear();
}
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `defaultProjectMatchedFiles.clear`
### `getProgramAndAST(parseSettings: ParseSettings, hasFullTypeInformation: boolean): ASTAndProgram`

<details><summary>Code</summary>

```ts
function getProgramAndAST(
  parseSettings: ParseSettings,
  hasFullTypeInformation: boolean,
): ASTAndProgram {
  if (parseSettings.projectService) {
    const fromProjectService = useProgramFromProjectService(
      parseSettings.projectService,
      parseSettings,
      hasFullTypeInformation,
      defaultProjectMatchedFiles,
    );
    if (fromProjectService) {
      return fromProjectService;
    }
  }

  if (parseSettings.programs) {
    const fromProvidedPrograms = useProvidedPrograms(
      parseSettings.programs,
      parseSettings,
    );
    if (fromProvidedPrograms) {
      return fromProvidedPrograms;
    }
  }

  // no need to waste time creating a program as the caller didn't want parser services
  // so we can save time and just create a lonesome source file
  if (!hasFullTypeInformation) {
    return createNoProgram(parseSettings);
  }

  return createProjectProgram(
    parseSettings,
    getWatchProgramsForProjects(parseSettings),
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * @param parseSettings Internal settings for parsing the file
 * @param hasFullTypeInformation True if the program should be attempted to be calculated from provided tsconfig files
 * @returns Returns a source file and program corresponding to the linted code
 */
```

- **Parameters**:
  - `parseSettings: ParseSettings`
  - `hasFullTypeInformation: boolean`
- **Return Type**: `ASTAndProgram`
- **Calls**:
  - `useProgramFromProjectService (from ./useProgramFromProjectService)`
  - `useProvidedPrograms (from ./create-program/useProvidedPrograms)`
  - `createNoProgram (from ./create-program/createSourceFile)`
  - `createProjectProgram (from ./create-program/createProjectProgram)`
  - `getWatchProgramsForProjects (from ./create-program/getWatchProgramsForProjects)`
- **Internal Comments**:
```
// no need to waste time creating a program as the caller didn't want parser services
// so we can save time and just create a lonesome source file
```

### `parse(code: string, options: T): AST<T>`

<details><summary>Code</summary>

```ts
export function parse<T extends TSESTreeOptions = TSESTreeOptions>(
  code: string,
  options?: T,
): AST<T> {
  const { ast } = parseWithNodeMapsInternal(code, options, false);
  return ast;
}
```
</details>

- **Parameters**:
  - `code: string`
  - `options: T`
- **Return Type**: `AST<T>`
- **Calls**:
  - `parseWithNodeMapsInternal`
### `parseWithNodeMapsInternal(code: string | ts.SourceFile, options: T | undefined, shouldPreserveNodeMaps: boolean): ParseWithNodeMapsResult<T>`

<details><summary>Code</summary>

```ts
function parseWithNodeMapsInternal<T extends TSESTreeOptions = TSESTreeOptions>(
  code: string | ts.SourceFile,
  options: T | undefined,
  shouldPreserveNodeMaps: boolean,
): ParseWithNodeMapsResult<T> {
  /**
   * Reset the parse configuration
   */
  const parseSettings = createParseSettings(code, options);

  /**
   * Ensure users do not attempt to use parse() when they need parseAndGenerateServices()
   */
  if (options?.errorOnTypeScriptSyntacticAndSemanticIssues) {
    throw new Error(
      `"errorOnTypeScriptSyntacticAndSemanticIssues" is only supported for parseAndGenerateServices()`,
    );
  }

  /**
   * Create a ts.SourceFile directly, no ts.Program is needed for a simple parse
   */
  const ast = createSourceFile(parseSettings);

  /**
   * Convert the TypeScript AST to an ESTree-compatible one
   */
  const { astMaps, estree } = astConverter(
    ast,
    parseSettings,
    shouldPreserveNodeMaps,
  );

  return {
    ast: estree as AST<T>,
    esTreeNodeToTSNodeMap: astMaps.esTreeNodeToTSNodeMap,
    tsNodeToESTreeNodeMap: astMaps.tsNodeToESTreeNodeMap,
  };
}
```
</details>

- **Parameters**:
  - `code: string | ts.SourceFile`
  - `options: T | undefined`
  - `shouldPreserveNodeMaps: boolean`
- **Return Type**: `ParseWithNodeMapsResult<T>`
- **Calls**:
  - `createParseSettings (from ./parseSettings/createParseSettings)`
  - `createSourceFile (from ./create-program/createSourceFile)`
  - `astConverter (from ./ast-converter)`
- **Internal Comments**:
```
/**
   * Reset the parse configuration
   */ (x2)
/**
   * Ensure users do not attempt to use parse() when they need parseAndGenerateServices()
   */
/**
   * Create a ts.SourceFile directly, no ts.Program is needed for a simple parse
   */ (x2)
/**
   * Convert the TypeScript AST to an ESTree-compatible one
   */ (x2)
```

### `clearParseAndGenerateServicesCalls(): void`

<details><summary>Code</summary>

```ts
export function clearParseAndGenerateServicesCalls(): void {
  parseAndGenerateServicesCalls = {};
}
```
</details>

- **Return Type**: `void`
### `parseAndGenerateServices(code: string | ts.SourceFile, tsestreeOptions: T): ParseAndGenerateServicesResult<T>`

<details><summary>Code</summary>

```ts
export function parseAndGenerateServices<
  T extends TSESTreeOptions = TSESTreeOptions,
>(
  code: string | ts.SourceFile,
  tsestreeOptions: T,
): ParseAndGenerateServicesResult<T> {
  /**
   * Reset the parse configuration
   */
  const parseSettings = createParseSettings(code, tsestreeOptions);

  /**
   * If this is a single run in which the user has not provided any existing programs but there
   * are programs which need to be created from the provided "project" option,
   * create an Iterable which will lazily create the programs as needed by the iteration logic
   */
  if (
    parseSettings.singleRun &&
    !parseSettings.programs &&
    parseSettings.projects.size > 0
  ) {
    parseSettings.programs = {
      *[Symbol.iterator](): Iterator<ts.Program> {
        for (const configFile of parseSettings.projects) {
          const existingProgram = existingPrograms.get(configFile[0]);
          if (existingProgram) {
            yield existingProgram;
          } else {
            log(
              'Detected single-run/CLI usage, creating Program once ahead of time for project: %s',
              configFile,
            );
            const newProgram = createProgramFromConfigFile(configFile[1]);
            existingPrograms.set(configFile[0], newProgram);
            yield newProgram;
          }
        }
      },
    };
  }

  const hasFullTypeInformation =
    parseSettings.programs != null ||
    parseSettings.projects.size > 0 ||
    !!parseSettings.projectService;

  if (
    typeof tsestreeOptions.errorOnTypeScriptSyntacticAndSemanticIssues ===
      'boolean' &&
    tsestreeOptions.errorOnTypeScriptSyntacticAndSemanticIssues
  ) {
    parseSettings.errorOnTypeScriptSyntacticAndSemanticIssues = true;
  }

  if (
    parseSettings.errorOnTypeScriptSyntacticAndSemanticIssues &&
    !hasFullTypeInformation
  ) {
    throw new Error(
      'Cannot calculate TypeScript semantic issues without a valid project.',
    );
  }

  /**
   * If we are in singleRun mode but the parseAndGenerateServices() function has been called more than once for the current file,
   * it must mean that we are in the middle of an ESLint automated fix cycle (in which parsing can be performed up to an additional
   * 10 times in order to apply all possible fixes for the file).
   *
   * In this scenario we cannot rely upon the singleRun AOT compiled programs because the SourceFiles will not contain the source
   * with the latest fixes applied. Therefore we fallback to creating the quickest possible isolated program from the updated source.
   */
  if (parseSettings.singleRun && tsestreeOptions.filePath) {
    parseAndGenerateServicesCalls[tsestreeOptions.filePath] =
      (parseAndGenerateServicesCalls[tsestreeOptions.filePath] || 0) + 1;
  }

  const { ast, program } =
    parseSettings.singleRun &&
    tsestreeOptions.filePath &&
    parseAndGenerateServicesCalls[tsestreeOptions.filePath] > 1
      ? createIsolatedProgram(parseSettings)
      : getProgramAndAST(parseSettings, hasFullTypeInformation);

  /**
   * Convert the TypeScript AST to an ESTree-compatible one, and optionally preserve
   * mappings between converted and original AST nodes
   */
  const shouldPreserveNodeMaps =
    typeof parseSettings.preserveNodeMaps === 'boolean'
      ? parseSettings.preserveNodeMaps
      : true;

  const { astMaps, estree } = astConverter(
    ast,
    parseSettings,
    shouldPreserveNodeMaps,
  );

  /**
   * Even if TypeScript parsed the source code ok, and we had no problems converting the AST,
   * there may be other syntactic or semantic issues in the code that we can optionally report on.
   */
  if (program && parseSettings.errorOnTypeScriptSyntacticAndSemanticIssues) {
    const error = getFirstSemanticOrSyntacticError(program, ast);
    if (error) {
      throw convertError(error);
    }
  }

  /**
   * Return the converted AST and additional parser services
   */
  return {
    ast: estree as AST<T>,
    services: createParserServices(astMaps, program),
  };
}
```
</details>

- **Parameters**:
  - `code: string | ts.SourceFile`
  - `tsestreeOptions: T`
- **Return Type**: `ParseAndGenerateServicesResult<T>`
- **Calls**:
  - `createParseSettings (from ./parseSettings/createParseSettings)`
  - `existingPrograms.get`
  - `log`
  - `createProgramFromConfigFile (from ./create-program/useProvidedPrograms)`
  - `existingPrograms.set`
  - `createIsolatedProgram (from ./create-program/createIsolatedProgram)`
  - `getProgramAndAST`
  - `astConverter (from ./ast-converter)`
  - `getFirstSemanticOrSyntacticError (from ./semantic-or-syntactic-errors)`
  - `convertError (from ./convert)`
  - `createParserServices (from ./createParserServices)`
- **Internal Comments**:
```
/**
   * Reset the parse configuration
   */ (x2)
/**
   * If this is a single run in which the user has not provided any existing programs but there
   * are programs which need to be created from the provided "project" option,
   * create an Iterable which will lazily create the programs as needed by the iteration logic
   */
/**
   * If we are in singleRun mode but the parseAndGenerateServices() function has been called more than once for the current file,
   * it must mean that we are in the middle of an ESLint automated fix cycle (in which parsing can be performed up to an additional
   * 10 times in order to apply all possible fixes for the file).
   *
   * In this scenario we cannot rely upon the singleRun AOT compiled programs because the SourceFiles will not contain the source
   * with the latest fixes applied. Therefore we fallback to creating the quickest possible isolated program from the updated source.
   */
/**
   * Convert the TypeScript AST to an ESTree-compatible one, and optionally preserve
   * mappings between converted and original AST nodes
   */ (x2)
/**
   * Even if TypeScript parsed the source code ok, and we had no problems converting the AST,
   * there may be other syntactic or semantic issues in the code that we can optionally report on.
   */
/**
   * Return the converted AST and additional parser services
   */
```


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ParseAndGenerateServicesResult<T extends TSESTreeOptions>`

<details><summary>Interface Code</summary>

```ts
export interface ParseAndGenerateServicesResult<T extends TSESTreeOptions> {
  ast: AST<T>;
  services: ParserServices;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ast` | `AST<T>` | ✗ |  |
| `services` | `ParserServices` | ✗ |  |

### `ParseWithNodeMapsResult<T extends TSESTreeOptions>`

<details><summary>Interface Code</summary>

```ts
interface ParseWithNodeMapsResult<T extends TSESTreeOptions>
  extends ParserServicesNodeMaps {
  ast: AST<T>;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ast` | `AST<T>` | ✗ |  |


---

## Type Aliases

### `AST<T extends TSESTreeOptions extends TSESTreeOptions>`

```ts
type AST<T extends TSESTreeOptions extends TSESTreeOptions> = (T['comment'] extends true
  ? { comments: TSESTree.Comment[] }
  : {}) &
  (T['tokens'] extends true ? { tokens: TSESTree.Token[] } : {}) &
  TSESTree.Program;
```


---