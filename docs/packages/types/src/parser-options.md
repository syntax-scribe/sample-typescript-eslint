[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `parser-options.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 2
- **Type Aliases**: 6

## 🛠️ File Location:
📂 **`packages/types/src/parser-options.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Program` | `typescript` |
| `Lib` | `./lib` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ProjectServiceOptions`

<details><summary>Interface Code</summary>

```ts
export interface ProjectServiceOptions {
  /**
   * Globs of files to allow running with the default project compiler options
   * despite not being matched by the project service.
   */
  allowDefaultProject?: string[];

  /**
   * Path to a TSConfig to use instead of TypeScript's default project configuration.
   * @default 'tsconfig.json'
   */
  defaultProject?: string;

  /**
   * Whether to allow TypeScript plugins as configured in the TSConfig.
   */
  loadTypeScriptPlugins?: boolean;

  /**
   * The maximum number of files {@link allowDefaultProject} may match.
   * Each file match slows down linting, so if you do need to use this, please
   * file an informative issue on typescript-eslint explaining why - so we can
   * help you avoid using it!
   * @default 8
   */
  maximumDefaultProjectFileMatchCount_THIS_WILL_SLOW_DOWN_LINTING?: number;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `allowDefaultProject` | `string[]` | ✓ |  |
| `defaultProject` | `string` | ✓ |  |
| `loadTypeScriptPlugins` | `boolean` | ✓ |  |
| `maximumDefaultProjectFileMatchCount_THIS_WILL_SLOW_DOWN_LINTING` | `number` | ✓ |  |

### `ParserOptions`

<details><summary>Interface Code</summary>

```ts
export interface ParserOptions {
  [additionalProperties: string]: unknown;
  cacheLifetime?: {
    glob?: CacheDurationSeconds;
  };

  // typescript-estree specific
  debugLevel?: DebugLevel;
  ecmaFeatures?:
    | {
        [key: string]: unknown;
        globalReturn?: boolean | undefined;
        jsx?: boolean | undefined;
      }
    | undefined;
  ecmaVersion?: EcmaVersion;

  // use emitDecoratorMetadata without specifying parserOptions.project
  emitDecoratorMetadata?: boolean;
  errorOnTypeScriptSyntacticAndSemanticIssues?: boolean;

  errorOnUnknownASTType?: boolean;
  // use experimentalDecorators without specifying parserOptions.project
  experimentalDecorators?: boolean;
  extraFileExtensions?: string[];
  filePath?: string;
  // use isolatedDeclarations without specifying parserOptions.project
  isolatedDeclarations?: boolean;
  jsDocParsingMode?: JSDocParsingMode;
  jsxFragmentName?: string | null;
  // scope-manager specific
  jsxPragma?: string | null;
  lib?: Lib[];
  programs?: Program[] | null;
  project?: boolean | string | string[] | null;
  projectFolderIgnoreList?: string[];
  projectService?: boolean | ProjectServiceOptions;
  range?: boolean;
  sourceType?: SourceType | undefined;
  tokens?: boolean;
  tsconfigRootDir?: string;

  warnOnUnsupportedTypeScriptVersion?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `cacheLifetime` | `{
    glob?: CacheDurationSeconds;
  }` | ✓ |  |
| `debugLevel` | `DebugLevel` | ✓ |  |
| `ecmaFeatures` | `| {
        [key: string]: unknown;
        globalReturn?: boolean | undefined;
        jsx?: boolean | undefined;
      }
    | undefined` | ✓ |  |
| `ecmaVersion` | `EcmaVersion` | ✓ |  |
| `emitDecoratorMetadata` | `boolean` | ✓ |  |
| `errorOnTypeScriptSyntacticAndSemanticIssues` | `boolean` | ✓ |  |
| `errorOnUnknownASTType` | `boolean` | ✓ |  |
| `experimentalDecorators` | `boolean` | ✓ |  |
| `extraFileExtensions` | `string[]` | ✓ |  |
| `filePath` | `string` | ✓ |  |
| `isolatedDeclarations` | `boolean` | ✓ |  |
| `jsDocParsingMode` | `JSDocParsingMode` | ✓ |  |
| `jsxFragmentName` | `string | null` | ✓ |  |
| `jsxPragma` | `string | null` | ✓ |  |
| `lib` | `Lib[]` | ✓ |  |
| `programs` | `Program[] | null` | ✓ |  |
| `project` | `boolean | string | string[] | null` | ✓ |  |
| `projectFolderIgnoreList` | `string[]` | ✓ |  |
| `projectService` | `boolean | ProjectServiceOptions` | ✓ |  |
| `range` | `boolean` | ✓ |  |
| `sourceType` | `SourceType | undefined` | ✓ |  |
| `tokens` | `boolean` | ✓ |  |
| `tsconfigRootDir` | `string` | ✓ |  |
| `warnOnUnsupportedTypeScriptVersion` | `boolean` | ✓ |  |


---

## Type Aliases

### `DebugLevel`

```ts
type DebugLevel = | boolean
  | ('eslint' | 'typescript' | 'typescript-eslint')[];
```

### `CacheDurationSeconds`

```ts
type CacheDurationSeconds = number | 'Infinity';
```

### `EcmaVersion`

```ts
type EcmaVersion = | 3
  | 5
  | 6
  | 7
  | 8
  | 9
  | 10
  | 11
  | 12
  | 13
  | 14
  | 15
  | 16
  | 2015
  | 2016
  | 2017
  | 2018
  | 2019
  | 2020
  | 2021
  | 2022
  | 2023
  | 2024
  | 2025
  | 'latest'
  | undefined;
```

### `SourceTypeClassic`

```ts
type SourceTypeClassic = 'module' | 'script';
```

### `SourceType`

```ts
type SourceType = 'commonjs' | SourceTypeClassic;
```

### `JSDocParsingMode`

```ts
type JSDocParsingMode = 'all' | 'none' | 'type-info';
```


---