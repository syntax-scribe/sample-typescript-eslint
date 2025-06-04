[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `ESLintShared.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 8 |
| 🧱 Classes | 1 |
| 📦 Imports | 2 |
| 📐 Interfaces | 13 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/utils/src/ts-eslint/eslint/ESLintShared.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Linter` | `../Linter` |
| `RuleMetaData` | `../Rule` |


---

## Functions

### `ESLintBase.calculateConfigForFile(filePath: string): Promise<Config>`

<details><summary>Code</summary>

```ts
calculateConfigForFile(filePath: string): Promise<Config>;
```
</details>

- **JSDoc**:
```ts
/**
   * This method calculates the configuration for a given file, which can be useful for debugging purposes.
   * - It resolves and merges extends and overrides settings into the top level configuration.
   * - It resolves the parser setting to absolute paths.
   * - It normalizes the plugins setting to align short names. (e.g., eslint-plugin-foo → foo)
   * - It adds the processor setting if a legacy file extension processor is matched.
   * - It doesn't interpret the env setting to the globals and parserOptions settings, so the result object contains
   *   the env setting as is.
   * @param filePath The path to the file whose configuration you would like to calculate. Directory paths are forbidden
   *                 because ESLint cannot handle the overrides setting.
   * @returns The promise that will be fulfilled with a configuration object.
   */
```

- **Parameters**:
  - `filePath: string`
- **Return Type**: `Promise<Config>`
### `ESLintBase.getRulesMetaForResults(results: LintResult[]): Record<string, RuleMetaData<string, Record<string, unknown>>>`

<details><summary>Code</summary>

```ts
getRulesMetaForResults(
    results: LintResult[],
  ): Record<string, RuleMetaData<string, Record<string, unknown>>>;
```
</details>

- **Parameters**:
  - `results: LintResult[]`
- **Return Type**: `Record<string, RuleMetaData<string, Record<string, unknown>>>`
### `ESLintBase.isPathIgnored(filePath: string): Promise<boolean>`

<details><summary>Code</summary>

```ts
isPathIgnored(filePath: string): Promise<boolean>;
```
</details>

- **JSDoc**:
```ts
/**
   * This method checks if a given file is ignored by your configuration.
   * @param filePath The path to the file you want to check.
   * @returns The promise that will be fulfilled with whether the file is ignored or not. If the file is ignored, then
   *          it will return true.
   */
```

- **Parameters**:
  - `filePath: string`
- **Return Type**: `Promise<boolean>`
### `ESLintBase.lintFiles(patterns: string | string[]): Promise<LintResult[]>`

<details><summary>Code</summary>

```ts
lintFiles(patterns: string | string[]): Promise<LintResult[]>;
```
</details>

- **JSDoc**:
```ts
/**
   * This method lints the files that match the glob patterns and then returns the results.
   * @param patterns The lint target files. This can contain any of file paths, directory paths, and glob patterns.
   * @returns The promise that will be fulfilled with an array of LintResult objects.
   */
```

- **Parameters**:
  - `patterns: string | string[]`
- **Return Type**: `Promise<LintResult[]>`
### `ESLintBase.lintText(code: string, options: LintTextOptions): Promise<LintResult[]>`

<details><summary>Code</summary>

```ts
lintText(code: string, options?: LintTextOptions): Promise<LintResult[]>;
```
</details>

- **JSDoc**:
```ts
/**
   * This method lints the given source code text and then returns the results.
   *
   * By default, this method uses the configuration that applies to files in the current working directory (the cwd
   * constructor option). If you want to use a different configuration, pass options.filePath, and ESLint will load the
   * same configuration that eslint.lintFiles() would use for a file at options.filePath.
   *
   * If the options.filePath value is configured to be ignored, this method returns an empty array. If the
   * options.warnIgnored option is set along with the options.filePath option, this method returns a LintResult object.
   * In that case, the result may contain a warning that indicates the file was ignored.
   * @param code The source code text to check.
   * @returns The promise that will be fulfilled with an array of LintResult objects. This is an array (despite there
   *          being only one lint result) in order to keep the interfaces between this and the eslint.lintFiles()
   *          method similar.
   */
```

- **Parameters**:
  - `code: string`
  - `options: LintTextOptions`
- **Return Type**: `Promise<LintResult[]>`
### `ESLintBase.loadFormatter(name: string): Promise<Formatter>`

<details><summary>Code</summary>

```ts
loadFormatter(name?: string): Promise<Formatter>;
```
</details>

- **JSDoc**:
```ts
/**
   * This method loads a formatter. Formatters convert lint results to a human- or machine-readable string.
   * @param name TThe path to the file you want to check.
   * The following values are allowed:
   * - undefined. In this case, loads the "stylish" built-in formatter.
   * - A name of built-in formatters.
   * - A name of third-party formatters. For examples:
   * -- `foo` will load eslint-formatter-foo.
   * -- `@foo` will load `@foo/eslint-formatter`.
   * -- `@foo/bar` will load `@foo/eslint-formatter-bar`.
   * - A path to the file that defines a formatter. The path must contain one or more path separators (/) in order to distinguish if it's a path or not. For example, start with ./.
   * @returns The promise that will be fulfilled with a Formatter object.
   */
```

- **Parameters**:
  - `name: string`
- **Return Type**: `Promise<Formatter>`
### `ESLintBase.getErrorResults(results: LintResult): LintResult`

<details><summary>Code</summary>

```ts
static getErrorResults(results: LintResult): LintResult;
```
</details>

- **JSDoc**:
```ts
/**
   * This method copies the given results and removes warnings. The returned value contains only errors.
   * @param results The LintResult objects to filter.
   * @returns The filtered LintResult objects.
   */
```

- **Parameters**:
  - `results: LintResult`
- **Return Type**: `LintResult`
### `ESLintBase.outputFixes(results: LintResult[]): Promise<void>`

<details><summary>Code</summary>

```ts
static outputFixes(results: LintResult[]): Promise<void>;
```
</details>

- **JSDoc**:
```ts
/**
   * This method writes code modified by ESLint's autofix feature into its respective file. If any of the modified
   * files don't exist, this method does nothing.
   * @param results The LintResult objects to write.
   * @returns The promise that will be fulfilled after all files are written.
   */
```

- **Parameters**:
  - `results: LintResult[]`
- **Return Type**: `Promise<void>`

---

## Classes

### `ESLintBase`

<details><summary>Class Code</summary>

```ts
export declare class ESLintBase<
  Config extends Linter.ConfigType,
  Options extends ESLintOptions<Config>,
> {
  /**
   * Creates a new instance of the main ESLint API.
   * @param options The options for this instance.
   */
  constructor(options?: Options);

  /**
   * This method calculates the configuration for a given file, which can be useful for debugging purposes.
   * - It resolves and merges extends and overrides settings into the top level configuration.
   * - It resolves the parser setting to absolute paths.
   * - It normalizes the plugins setting to align short names. (e.g., eslint-plugin-foo → foo)
   * - It adds the processor setting if a legacy file extension processor is matched.
   * - It doesn't interpret the env setting to the globals and parserOptions settings, so the result object contains
   *   the env setting as is.
   * @param filePath The path to the file whose configuration you would like to calculate. Directory paths are forbidden
   *                 because ESLint cannot handle the overrides setting.
   * @returns The promise that will be fulfilled with a configuration object.
   */
  calculateConfigForFile(filePath: string): Promise<Config>;

  getRulesMetaForResults(
    results: LintResult[],
  ): Record<string, RuleMetaData<string, Record<string, unknown>>>;

  /**
   * This method checks if a given file is ignored by your configuration.
   * @param filePath The path to the file you want to check.
   * @returns The promise that will be fulfilled with whether the file is ignored or not. If the file is ignored, then
   *          it will return true.
   */
  isPathIgnored(filePath: string): Promise<boolean>;

  /**
   * This method lints the files that match the glob patterns and then returns the results.
   * @param patterns The lint target files. This can contain any of file paths, directory paths, and glob patterns.
   * @returns The promise that will be fulfilled with an array of LintResult objects.
   */
  lintFiles(patterns: string | string[]): Promise<LintResult[]>;

  /**
   * This method lints the given source code text and then returns the results.
   *
   * By default, this method uses the configuration that applies to files in the current working directory (the cwd
   * constructor option). If you want to use a different configuration, pass options.filePath, and ESLint will load the
   * same configuration that eslint.lintFiles() would use for a file at options.filePath.
   *
   * If the options.filePath value is configured to be ignored, this method returns an empty array. If the
   * options.warnIgnored option is set along with the options.filePath option, this method returns a LintResult object.
   * In that case, the result may contain a warning that indicates the file was ignored.
   * @param code The source code text to check.
   * @returns The promise that will be fulfilled with an array of LintResult objects. This is an array (despite there
   *          being only one lint result) in order to keep the interfaces between this and the eslint.lintFiles()
   *          method similar.
   */
  lintText(code: string, options?: LintTextOptions): Promise<LintResult[]>;

  /**
   * This method loads a formatter. Formatters convert lint results to a human- or machine-readable string.
   * @param name TThe path to the file you want to check.
   * The following values are allowed:
   * - undefined. In this case, loads the "stylish" built-in formatter.
   * - A name of built-in formatters.
   * - A name of third-party formatters. For examples:
   * -- `foo` will load eslint-formatter-foo.
   * -- `@foo` will load `@foo/eslint-formatter`.
   * -- `@foo/bar` will load `@foo/eslint-formatter-bar`.
   * - A path to the file that defines a formatter. The path must contain one or more path separators (/) in order to distinguish if it's a path or not. For example, start with ./.
   * @returns The promise that will be fulfilled with a Formatter object.
   */
  loadFormatter(name?: string): Promise<Formatter>;

  ////////////////////
  // static members //
  ////////////////////

  /**
   * This method copies the given results and removes warnings. The returned value contains only errors.
   * @param results The LintResult objects to filter.
   * @returns The filtered LintResult objects.
   */
  static getErrorResults(results: LintResult): LintResult;
  /**
   * This method writes code modified by ESLint's autofix feature into its respective file. If any of the modified
   * files don't exist, this method does nothing.
   * @param results The LintResult objects to write.
   * @returns The promise that will be fulfilled after all files are written.
   */
  static outputFixes(results: LintResult[]): Promise<void>;
  /**
   * The version text.
   */
  static readonly version: string;
  /**
   * The type of configuration used by this class.
   */
  static readonly configType: Linter.ConfigTypeSpecifier;
}
```
</details>

#### Methods

##### `calculateConfigForFile(filePath: string): Promise<Config>`

<details><summary>Code</summary>

```ts
calculateConfigForFile(filePath: string): Promise<Config>;
```
</details>

##### `getRulesMetaForResults(results: LintResult[]): Record<string, RuleMetaData<string, Record<string, unknown>>>`

<details><summary>Code</summary>

```ts
getRulesMetaForResults(
    results: LintResult[],
  ): Record<string, RuleMetaData<string, Record<string, unknown>>>;
```
</details>

##### `isPathIgnored(filePath: string): Promise<boolean>`

<details><summary>Code</summary>

```ts
isPathIgnored(filePath: string): Promise<boolean>;
```
</details>

##### `lintFiles(patterns: string | string[]): Promise<LintResult[]>`

<details><summary>Code</summary>

```ts
lintFiles(patterns: string | string[]): Promise<LintResult[]>;
```
</details>

##### `lintText(code: string, options: LintTextOptions): Promise<LintResult[]>`

<details><summary>Code</summary>

```ts
lintText(code: string, options?: LintTextOptions): Promise<LintResult[]>;
```
</details>

##### `loadFormatter(name: string): Promise<Formatter>`

<details><summary>Code</summary>

```ts
loadFormatter(name?: string): Promise<Formatter>;
```
</details>

##### `getErrorResults(results: LintResult): LintResult`

<details><summary>Code</summary>

```ts
static getErrorResults(results: LintResult): LintResult;
```
</details>

##### `outputFixes(results: LintResult[]): Promise<void>`

<details><summary>Code</summary>

```ts
static outputFixes(results: LintResult[]): Promise<void>;
```
</details>


---

## Interfaces

### `ESLintOptions<Config extends Linter.ConfigType>`

<details><summary>Interface Code</summary>

```ts
export interface ESLintOptions<Config extends Linter.ConfigType> {
  /**
   * If false is present, ESLint suppresses directive comments in source code.
   * If this option is false, it overrides the noInlineConfig setting in your configurations.
   * @default true
   */
  allowInlineConfig?: boolean;
  /**
   * Configuration object, extended by all configurations used with this instance.
   * You can use this option to define the default settings that will be used if your configuration files don't
   * configure it.
   * @default null
   */
  baseConfig?: Config | null;
  /**
   * If `true` is present, the `eslint.lintFiles()` method caches lint results and uses it if each target file is not
   * changed. Please mind that ESLint doesn't clear the cache when you upgrade ESLint plugins. In that case, you have
   * to remove the cache file manually. The `eslint.lintText()` method doesn't use caches even if you pass the
   * options.filePath to the method.
   * @default false
   */
  cache?: boolean;
  /**
   * The eslint.lintFiles() method writes caches into this file.
   * @default '.eslintcache'
   */
  cacheLocation?: string;
  /**
   * Strategy for the cache to use for detecting changed files.
   * @default 'metadata'
   */
  cacheStrategy?: 'content' | 'metadata';
  /**
   * The working directory. This must be an absolute path.
   * @default process.cwd()
   */
  cwd?: string;
  /**
   * Unless set to false, the `eslint.lintFiles()` method will throw an error when no target files are found.
   * @default true
   */
  errorOnUnmatchedPattern?: boolean;
  /**
   * If `true` is present, the `eslint.lintFiles()` and `eslint.lintText()` methods work in autofix mode.
   * If a predicate function is present, the methods pass each lint message to the function, then use only the
   * lint messages for which the function returned true.
   * @default false
   */
  fix?: boolean | ((message: LintMessage) => boolean);
  /**
   * The types of the rules that the `eslint.lintFiles()` and `eslint.lintText()` methods use for autofix.
   * @default null
   */
  fixTypes?: ('directive' | 'problem' | 'suggestion')[] | null;
  /**
   * If false is present, the `eslint.lintFiles()` method doesn't interpret glob patterns.
   * @default true
   */
  globInputPaths?: boolean;
  /**
   * Configuration object, overrides all configurations used with this instance.
   * You can use this option to define the settings that will be used even if your configuration files configure it.
   * @default null
   */
  overrideConfig?: Config | null;
  /**
   * When set to true, missing patterns cause the linting operation to short circuit and not report any failures.
   * @default false
   */
  passOnNoPatterns?: boolean;
  /**
   * The plugin implementations that ESLint uses for the plugins setting of your configuration.
   * This is a map-like object. Those keys are plugin IDs and each value is implementation.
   * @default null
   */
  plugins?: Record<string, Linter.Plugin> | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `allowInlineConfig` | `boolean` | ✓ |  |
| `baseConfig` | `Config | null` | ✓ |  |
| `cache` | `boolean` | ✓ |  |
| `cacheLocation` | `string` | ✓ |  |
| `cacheStrategy` | `'content' | 'metadata'` | ✓ |  |
| `cwd` | `string` | ✓ |  |
| `errorOnUnmatchedPattern` | `boolean` | ✓ |  |
| `fix` | `boolean | ((message: LintMessage) => boolean)` | ✓ |  |
| `fixTypes` | `('directive' | 'problem' | 'suggestion')[] | null` | ✓ |  |
| `globInputPaths` | `boolean` | ✓ |  |
| `overrideConfig` | `Config | null` | ✓ |  |
| `passOnNoPatterns` | `boolean` | ✓ |  |
| `plugins` | `Record<string, Linter.Plugin> | null` | ✓ |  |

### `DeprecatedRuleInfo`

<details><summary>Interface Code</summary>

```ts
export interface DeprecatedRuleInfo {
  /**
   *  The rule IDs that replace this deprecated rule.
   */
  replacedBy: string[];
  /**
   *  The rule ID.
   */
  ruleId: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `replacedBy` | `string[]` | ✗ |  |
| `ruleId` | `string` | ✗ |  |

### `LintResult`

<details><summary>Interface Code</summary>

```ts
export interface LintResult {
  /**
   * The number of errors. This includes fixable errors.
   */
  errorCount: number;
  /**
   * The number of fatal errors.
   */
  fatalErrorCount: number;
  /**
   * The absolute path to the file of this result. This is the string "<text>" if the file path is unknown (when you
   * didn't pass the options.filePath option to the eslint.lintText() method).
   */
  filePath: string;
  /**
   * The number of errors that can be fixed automatically by the fix constructor option.
   */
  fixableErrorCount: number;
  /**
   * The number of warnings that can be fixed automatically by the fix constructor option.
   */
  fixableWarningCount: number;
  /**
   * The array of LintMessage objects.
   */
  messages: LintMessage[];
  /**
   * The source code of the file that was linted, with as many fixes applied as possible.
   */
  output?: string;
  /**
   * The original source code text. This property is undefined if any messages didn't exist or the output
   * property exists.
   */
  source?: string;
  /**
   * Timing information of the lint run.
   * This exists if and only if the `--stats` CLI flag was added or the `stats: true`
   * option was passed to the ESLint class
   * @since 9.0.0
   */
  stats?: LintStats;
  /**
   * The array of SuppressedLintMessage objects.
   */
  suppressedMessages: SuppressedLintMessage[];
  /**
   * The information about the deprecated rules that were used to check this file.
   */
  usedDeprecatedRules: DeprecatedRuleInfo[];
  /**
   * The number of warnings. This includes fixable warnings.
   */
  warningCount: number;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `errorCount` | `number` | ✗ |  |
| `fatalErrorCount` | `number` | ✗ |  |
| `filePath` | `string` | ✗ |  |
| `fixableErrorCount` | `number` | ✗ |  |
| `fixableWarningCount` | `number` | ✗ |  |
| `messages` | `LintMessage[]` | ✗ |  |
| `output` | `string` | ✓ |  |
| `source` | `string` | ✓ |  |
| `stats` | `LintStats` | ✓ |  |
| `suppressedMessages` | `SuppressedLintMessage[]` | ✗ |  |
| `usedDeprecatedRules` | `DeprecatedRuleInfo[]` | ✗ |  |
| `warningCount` | `number` | ✗ |  |

### `LintStats`

<details><summary>Interface Code</summary>

```ts
export interface LintStats {
  /**
   * The number of times ESLint has applied at least one fix after linting.
   */
  fixPasses: number;
  /**
   * The times spent on (parsing, fixing, linting) a file, where the linting refers to the timing information for each rule.
   */
  times: {
    passes: LintStatsTimePass[];
  };
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `fixPasses` | `number` | ✗ |  |
| `times` | `{
    passes: LintStatsTimePass[];
  }` | ✗ |  |

### `LintStatsTimePass`

<details><summary>Interface Code</summary>

```ts
export interface LintStatsTimePass {
  /**
   * The total time that is spent on applying fixes to the code.
   */
  fix: LintStatsFixTime;
  /**
   * The total time that is spent when parsing a file.
   */
  parse: LintStatsParseTime;
  /**
   * The total time that is spent on a rule.
   */
  rules?: Record<string, LintStatsRuleTime>;
  /**
   * The cumulative total
   */
  total: number;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `fix` | `LintStatsFixTime` | ✗ |  |
| `parse` | `LintStatsParseTime` | ✗ |  |
| `rules` | `Record<string, LintStatsRuleTime>` | ✓ |  |
| `total` | `number` | ✗ |  |

### `LintStatsParseTime`

<details><summary>Interface Code</summary>

```ts
export interface LintStatsParseTime {
  total: number;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `total` | `number` | ✗ |  |

### `LintStatsRuleTime`

<details><summary>Interface Code</summary>

```ts
export interface LintStatsRuleTime {
  total: number;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `total` | `number` | ✗ |  |

### `LintStatsFixTime`

<details><summary>Interface Code</summary>

```ts
export interface LintStatsFixTime {
  total: number;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `total` | `number` | ✗ |  |

### `LintTextOptions`

<details><summary>Interface Code</summary>

```ts
export interface LintTextOptions {
  /**
   * The path to the file of the source code text. If omitted, the result.filePath becomes the string "<text>".
   */
  filePath?: string;
  /**
   * If true is present and the options.filePath is a file ESLint should ignore, this method returns a lint result
   * contains a warning message.
   */
  warnIgnored?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `filePath` | `string` | ✓ |  |
| `warnIgnored` | `boolean` | ✓ |  |

### `LintMessage`

<details><summary>Interface Code</summary>

```ts
export interface LintMessage {
  /**
   * The 1-based column number of the begin point of this message.
   */
  column: number | undefined;
  /**
   * The 1-based column number of the end point of this message. This property is undefined if this message
   * is not a range.
   */
  endColumn: number | undefined;
  /**
   * The 1-based line number of the end point of this message. This property is undefined if this
   * message is not a range.
   */
  endLine: number | undefined;
  /**
   * `true` if this is a fatal error unrelated to a rule, like a parsing error.
   */
  fatal?: boolean | undefined;
  /**
   * The EditInfo object of autofix. This property is undefined if this message is not fixable.
   */
  fix: EditInfo | undefined;
  /**
   * The 1-based line number of the begin point of this message.
   */
  line: number | undefined;
  /**
   * The error message
   */
  message: string;
  /**
   * The rule name that generates this lint message. If this message is generated by the ESLint core rather than
   * rules, this is null.
   */
  ruleId: string | null;
  /**
   * The severity of this message. 1 means warning and 2 means error.
   */
  severity: 1 | 2;
  /**
   * The list of suggestions. Each suggestion is the pair of a description and an EditInfo object to fix code. API
   * users such as editor integrations can choose one of them to fix the problem of this message. This property is
   * undefined if this message doesn't have any suggestions.
   */
  suggestions:
    | {
        desc: string;
        fix: EditInfo;
      }[]
    | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `column` | `number | undefined` | ✗ |  |
| `endColumn` | `number | undefined` | ✗ |  |
| `endLine` | `number | undefined` | ✗ |  |
| `fatal` | `boolean | undefined` | ✓ |  |
| `fix` | `EditInfo | undefined` | ✗ |  |
| `line` | `number | undefined` | ✗ |  |
| `message` | `string` | ✗ |  |
| `ruleId` | `string | null` | ✗ |  |
| `severity` | `1 | 2` | ✗ |  |
| `suggestions` | `| {
        desc: string;
        fix: EditInfo;
      }[]
    | undefined` | ✗ |  |

### `SuppressedLintMessage`

<details><summary>Interface Code</summary>

```ts
export interface SuppressedLintMessage extends LintMessage {
  /**
   * The list of suppressions.
   */
  suppressions?: {
    /**
     * The free text description added after the `--` in the comment
     */
    justification: string;
    /**
     * Right now, this is always `directive`
     */
    kind: string;
  }[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `suppressions` | `{
    /**
     * The free text description added after the `--` in the comment
     */
    justification: string;
    /**
     * Right now, this is always `directive`
     */
    kind: string;
  }[]` | ✓ |  |

### `EditInfo`

<details><summary>Interface Code</summary>

```ts
export interface EditInfo {
  /**
   * The pair of 0-based indices in source code text to remove.
   */
  range: [number, number];
  /**
   * The text to add.
   */
  text: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `range` | `[number, number]` | ✗ |  |
| `text` | `string` | ✗ |  |

### `Formatter`

<details><summary>Interface Code</summary>

```ts
export interface Formatter {
  /**
   * The method to convert the LintResult objects to text.
   * Promise return supported since 8.4.0
   */
  format(results: LintResult[]): string | Promise<string>;
}
```
</details>


---