[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `FlatESLint.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 2 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 13 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/utils/src/ts-eslint/eslint/FlatESLint.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintFlatESLint` | `eslint/use-at-your-own-risk` |
| `FlatConfig` | `../Config` |


---

## Functions

### `FlatESLintBase.calculateConfigForFile(filePath: string): Promise<FlatConfig.ConfigArray>`

<details><summary>Code</summary>

```ts
calculateConfigForFile(filePath: string): Promise<FlatConfig.ConfigArray>;
```
</details>

- **JSDoc**:
```ts
/**
   * Returns a configuration object for the given file based on the CLI options.
   * This is the same logic used by the ESLint CLI executable to determine
   * configuration for each file it processes.
   * @param filePath The path of the file to retrieve a config object for.
   * @returns A configuration object for the file or `undefined` if there is no configuration data for the object.
   */
```

- **Parameters**:
  - `filePath: string`
- **Return Type**: `Promise<FlatConfig.ConfigArray>`
### `FlatESLintBase.findConfigFile(): Promise<string | undefined>`

<details><summary>Code</summary>

```ts
findConfigFile(): Promise<string | undefined>;
```
</details>

- **JSDoc**:
```ts
/**
   * Finds the config file being used by this instance based on the options
   * passed to the constructor.
   * @returns The path to the config file being used or `undefined` if no config file is being used.
   */
```

- **Return Type**: `Promise<string | undefined>`

---

## Classes

### `FlatESLintBase`

<details><summary>Class Code</summary>

```ts
declare class FlatESLintBase extends Shared.ESLintBase<
  FlatConfig.ConfigArray,
  FlatESLint.ESLintOptions
> {
  static readonly configType: 'flat';

  /**
   * Returns a configuration object for the given file based on the CLI options.
   * This is the same logic used by the ESLint CLI executable to determine
   * configuration for each file it processes.
   * @param filePath The path of the file to retrieve a config object for.
   * @returns A configuration object for the file or `undefined` if there is no configuration data for the object.
   */
  calculateConfigForFile(filePath: string): Promise<FlatConfig.ConfigArray>;

  /**
   * Finds the config file being used by this instance based on the options
   * passed to the constructor.
   * @returns The path to the config file being used or `undefined` if no config file is being used.
   */
  findConfigFile(): Promise<string | undefined>;
}
```
</details>

#### Methods

##### `calculateConfigForFile(filePath: string): Promise<FlatConfig.ConfigArray>`

<details><summary>Code</summary>

```ts
calculateConfigForFile(filePath: string): Promise<FlatConfig.ConfigArray>;
```
</details>

##### `findConfigFile(): Promise<string | undefined>`

<details><summary>Code</summary>

```ts
findConfigFile(): Promise<string | undefined>;
```
</details>

### `FlatESLint`

<details><summary>Class Code</summary>

```ts
export class FlatESLint extends (ESLintFlatESLint as typeof FlatESLintBase) {}
```
</details>


---

## Interfaces

### `ESLintOptions`

<details><summary>Interface Code</summary>

```ts
export interface ESLintOptions
    extends Shared.ESLintOptions<FlatConfig.ConfigArray> {
    /**
     * If false is present, the eslint.lintFiles() method doesn't respect `ignorePatterns` ignorePatterns in your configuration.
     * @default true
     */
    ignore?: boolean;
    /**
     * Ignore file patterns to use in addition to config ignores. These patterns are relative to cwd.
     * @default null
     */
    ignorePatterns?: string[] | null;
    /**
     * The path to a configuration file, overrides all configurations used with this instance.
     * The options.overrideConfig option is applied after this option is applied.
     * Searches for default config file when falsy; doesn't do any config file lookup when `true`; considered to be a config filename when a string.
     * @default false
     */
    overrideConfigFile?: boolean | string;
    /**
     * A predicate function that filters rules to be run.
     * This function is called with an object containing `ruleId` and `severity`, and returns `true` if the rule should be run.
     * @default () => true
     */
    ruleFilter?: RuleFilter;
    /**
     * When set to true, additional statistics are added to the lint results.
     * @see {@link https://eslint.org/docs/latest/extend/stats}
     * @default false
     */
    stats?: boolean;
    /**
     * Show warnings when the file list includes ignored files.
     * @default true
     */
    warnIgnored?: boolean;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ignore` | `boolean` | ✓ |  |
| `ignorePatterns` | `string[] | null` | ✓ |  |
| `overrideConfigFile` | `boolean | string` | ✓ |  |
| `ruleFilter` | `RuleFilter` | ✓ |  |
| `stats` | `boolean` | ✓ |  |
| `warnIgnored` | `boolean` | ✓ |  |


---

## Type Aliases

### `DeprecatedRuleInfo`

```ts
type DeprecatedRuleInfo = Shared.DeprecatedRuleInfo;
```

### `EditInfo`

```ts
type EditInfo = Shared.EditInfo;
```

### `Formatter`

```ts
type Formatter = Shared.Formatter;
```

### `LintMessage`

```ts
type LintMessage = Shared.LintMessage;
```

### `LintResult`

```ts
type LintResult = Shared.LintResult;
```

### `LintStats`

```ts
type LintStats = Shared.LintStats;
```

### `LintStatsFixTime`

```ts
type LintStatsFixTime = Shared.LintStatsFixTime;
```

### `LintStatsParseTime`

```ts
type LintStatsParseTime = Shared.LintStatsParseTime;
```

### `LintStatsRuleTime`

```ts
type LintStatsRuleTime = Shared.LintStatsRuleTime;
```

### `LintStatsTimePass`

```ts
type LintStatsTimePass = Shared.LintStatsTimePass;
```

### `LintTextOptions`

```ts
type LintTextOptions = Shared.LintTextOptions;
```

### `SuppressedLintMessage`

```ts
type SuppressedLintMessage = Shared.SuppressedLintMessage;
```

### `RuleFilter`

```ts
type RuleFilter = (rule: {
    ruleId: string;
    severity: number;
  }) => boolean;
```


---