[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Config.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 12 |
| 📑 Type Aliases | 38 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/utils/src/ts-eslint/Config.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserType` | `./Parser` |
| `ProcessorType` | `./Processor` |
| `LooseRuleDefinition` | `./Rule` |
| `SharedConfigurationSettings` | `./Rule` |


---

## 🔧 Functions

> No functions found in this file.


---

## Interfaces

### `GlobalsConfig`

<details><summary>Interface Code</summary>

```ts
export interface GlobalsConfig {
    [name: string]: GlobalVariableOption;
  }
```
</details>

### `EnvironmentConfig`

<details><summary>Interface Code</summary>

```ts
export interface EnvironmentConfig {
    [name: string]: boolean;
  }
```
</details>

### `PluginMeta`

<details><summary>Interface Code</summary>

```ts
export interface PluginMeta {
    /**
     * The meta.name property should match the npm package name for your plugin.
     */
    name: string;
    /**
     * The meta.version property should match the npm package version for your plugin.
     */
    version: string;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `name` | `string` | ✗ |  |
| `version` | `string` | ✗ |  |

### `BaseConfig`

<details><summary>Interface Code</summary>

```ts
interface BaseConfig {
    $schema?: string;
    /**
     * The environment settings.
     */
    env?: EnvironmentConfig;
    /**
     * The path to other config files or the package name of shareable configs.
     */
    extends?: string | string[];
    /**
     * The global variable settings.
     */
    globals?: GlobalsConfig;
    /**
     * The flag that disables directive comments.
     */
    noInlineConfig?: boolean;
    /**
     * The override settings per kind of files.
     */
    overrides?: ConfigOverride[];
    /**
     * The path to a parser or the package name of a parser.
     */
    parser?: string | null;
    /**
     * The parser options.
     */
    parserOptions?: ParserOptions;
    /**
     * The plugin specifiers.
     */
    plugins?: string[];
    /**
     * The processor specifier.
     */
    processor?: string;
    /**
     * The flag to report unused `eslint-disable` comments.
     */
    reportUnusedDisableDirectives?: boolean;
    /**
     * The rule settings.
     */
    rules?: RulesRecord;
    /**
     * The shared settings.
     */
    settings?: SharedConfigurationSettings;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `$schema` | `string` | ✓ |  |
| `env` | `EnvironmentConfig` | ✓ |  |
| `extends` | `string | string[]` | ✓ |  |
| `globals` | `GlobalsConfig` | ✓ |  |
| `noInlineConfig` | `boolean` | ✓ |  |
| `overrides` | `ConfigOverride[]` | ✓ |  |
| `parser` | `string | null` | ✓ |  |
| `parserOptions` | `ParserOptions` | ✓ |  |
| `plugins` | `string[]` | ✓ |  |
| `processor` | `string` | ✓ |  |
| `reportUnusedDisableDirectives` | `boolean` | ✓ |  |
| `rules` | `RulesRecord` | ✓ |  |
| `settings` | `SharedConfigurationSettings` | ✓ |  |

### `ConfigOverride`

<details><summary>Interface Code</summary>

```ts
export interface ConfigOverride extends BaseConfig {
    excludedFiles?: string | string[];
    files: string | string[];
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `excludedFiles` | `string | string[]` | ✓ |  |
| `files` | `string | string[]` | ✗ |  |

### `Config`

<details><summary>Interface Code</summary>

```ts
export interface Config extends BaseConfig {
    /**
     * The glob patterns that ignore to lint.
     */
    ignorePatterns?: string | string[];
    /**
     * The root flag.
     */
    root?: boolean;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ignorePatterns` | `string | string[]` | ✓ |  |
| `root` | `boolean` | ✓ |  |

### `SharedConfigs`

<details><summary>Interface Code</summary>

```ts
export interface SharedConfigs {
    [key: string]: Config | ConfigArray;
  }
```
</details>

### `Plugin`

<details><summary>Interface Code</summary>

```ts
export interface Plugin {
    /**
     * Shared configurations bundled with the plugin.
     * Users will reference these directly in their config (i.e. `plugin.configs.recommended`).
     */
    configs?: SharedConfigs;
    /**
     * Metadata about your plugin for easier debugging and more effective caching of plugins.
     */
    meta?: { [K in keyof PluginMeta]?: PluginMeta[K] | undefined };
    /**
     * The definition of plugin processors.
     * Users can stringly reference the processor using the key in their config (i.e., `"pluginName/processorName"`).
     */
    processors?: Partial<Record<string, Processor>> | undefined;
    /**
     * The definition of plugin rules.
     * The key must be the name of the rule that users will use
     * Users can stringly reference the rule using the key they registered the plugin under combined with the rule name.
     * i.e. for the user config `plugins: { foo: pluginReference }` - the reference would be `"foo/ruleName"`.
     */
    rules?: Record<string, LooseRuleDefinition> | undefined;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `configs` | `SharedConfigs` | ✓ |  |
| `meta` | `{ [K in keyof PluginMeta]?: PluginMeta[K] | undefined }` | ✓ |  |
| `processors` | `Partial<Record<string, Processor>> | undefined` | ✓ |  |
| `rules` | `Record<string, LooseRuleDefinition> | undefined` | ✓ |  |

### `Plugins`

<details><summary>Interface Code</summary>

```ts
export interface Plugins {
    /**
     * We intentionally omit the `configs` key from this object because it avoids
     * type conflicts with old plugins that haven't updated their configs to flat configs yet.
     * It's valid to reference these old plugins because ESLint won't access the
     * `.config` property of a plugin when evaluating a flat config.
     */
    [pluginAlias: string]: Omit<Plugin, 'configs'>;
  }
```
</details>

### `LinterOptions`

<details><summary>Interface Code</summary>

```ts
export interface LinterOptions {
    /**
     * A Boolean value indicating if inline configuration is allowed.
     */
    noInlineConfig?: boolean;
    /**
     * A severity string indicating if and how unused disable and enable
     * directives should be tracked and reported. For legacy compatibility, `true`
     * is equivalent to `"warn"` and `false` is equivalent to `"off"`.
     * @default "off"
     */
    reportUnusedDisableDirectives?:
      | boolean
      | SharedConfig.Severity
      | SharedConfig.SeverityString;
    /**
     * A severity string indicating if and how unused inline directives
     * should be tracked and reported.
     *
     * since ESLint 9.19.0
     * @default "off"
     */
    reportUnusedInlineConfigs?:
      | SharedConfig.Severity
      | SharedConfig.SeverityString;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `noInlineConfig` | `boolean` | ✓ |  |
| `reportUnusedDisableDirectives` | `| boolean
      | SharedConfig.Severity
      | SharedConfig.SeverityString` | ✓ |  |
| `reportUnusedInlineConfigs` | `| SharedConfig.Severity
      | SharedConfig.SeverityString` | ✓ |  |

### `LanguageOptions`

<details><summary>Interface Code</summary>

```ts
export interface LanguageOptions {
    /**
     * The version of ECMAScript to support.
     * May be any year (i.e., `2022`) or version (i.e., `5`).
     * Set to `"latest"` for the most recent supported version.
     * @default "latest"
     */
    ecmaVersion?: EcmaVersion | undefined;
    /**
     * An object specifying additional objects that should be added to the global scope during linting.
     */
    globals?: GlobalsConfig | undefined;
    /**
     * An object containing a `parse()` method or a `parseForESLint()` method.
     * @default
     * ```
     * // https://github.com/eslint/espree
     * require('espree')
     * ```
     */
    parser?: Parser | undefined;
    /**
     * An object specifying additional options that are passed directly to the parser.
     * The available options are parser-dependent.
     */
    parserOptions?: ParserOptions | undefined;
    /**
     * The type of JavaScript source code.
     * Possible values are `"script"` for traditional script files, `"module"` for ECMAScript modules (ESM), and `"commonjs"` for CommonJS files.
     * @default
     * ```
     * // for `.js` and `.mjs` files
     * "module"
     * // for `.cjs` files
     * "commonjs"
     * ```
     */
    sourceType?: SourceType | undefined;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ecmaVersion` | `EcmaVersion | undefined` | ✓ |  |
| `globals` | `GlobalsConfig | undefined` | ✓ |  |
| `parser` | `Parser | undefined` | ✓ |  |
| `parserOptions` | `ParserOptions | undefined` | ✓ |  |
| `sourceType` | `SourceType | undefined` | ✓ |  |

### `Config`

<details><summary>Interface Code</summary>

```ts
export interface Config {
    /**
     * An array of glob patterns indicating the files that the configuration object should apply to.
     * If not specified, the configuration object applies to all files matched by any other configuration object.
     */
    files?: (
      | string
      | string[] // yes, a single layer of array nesting is supported
    )[];
    /**
     * An array of glob patterns indicating the files that the configuration object should not apply to.
     * If not specified, the configuration object applies to all files matched by files.
     */
    ignores?: string[];
    /**
     * Language specifier in the form `namespace/language-name` where `namespace` is a plugin name set in the `plugins` field.
     */
    language?: string;
    /**
     * An object containing settings related to how JavaScript is configured for linting.
     */
    languageOptions?: LanguageOptions;
    /**
     * An object containing settings related to the linting process.
     */
    linterOptions?: LinterOptions;
    /**
     * An string to identify the configuration object. Used in error messages and inspection tools.
     */
    name?: string;
    /**
     * An object containing a name-value mapping of plugin names to plugin objects.
     * When `files` is specified, these plugins are only available to the matching files.
     */
    plugins?: Plugins;
    /**
     * Either an object containing `preprocess()` and `postprocess()` methods or
     * a string indicating the name of a processor inside of a plugin
     * (i.e., `"pluginName/processorName"`).
     */
    processor?: string | Processor;
    /**
     * An object containing the configured rules.
     * When `files` or `ignores` are specified, these rule configurations are only available to the matching files.
     */
    rules?: Rules;
    /**
     * An object containing name-value pairs of information that should be available to all rules.
     */
    settings?: Settings;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `files` | `(
      | string
      | string[] // yes, a single layer of array nesting is supported
    )[]` | ✓ |  |
| `ignores` | `string[]` | ✓ |  |
| `language` | `string` | ✓ |  |
| `languageOptions` | `LanguageOptions` | ✓ |  |
| `linterOptions` | `LinterOptions` | ✓ |  |
| `name` | `string` | ✓ |  |
| `plugins` | `Plugins` | ✓ |  |
| `processor` | `string | Processor` | ✓ |  |
| `rules` | `Rules` | ✓ |  |
| `settings` | `Settings` | ✓ |  |


---

## Type Aliases

### `Severity`

```ts
type Severity = 0 | 1 | 2;
```

### `SeverityString`

```ts
type SeverityString = 'error' | 'off' | 'warn';
```

### `RuleLevel`

```ts
type RuleLevel = Severity | SeverityString;
```

### `RuleLevelAndOptions`

```ts
type RuleLevelAndOptions = [RuleLevel, ...unknown[]];
```

### `RuleEntry`

```ts
type RuleEntry = RuleLevel | RuleLevelAndOptions;
```

### `RulesRecord`

```ts
type RulesRecord = Partial<Record<string, RuleEntry>>;
```

### `GlobalVariableOptionBase`

```ts
type GlobalVariableOptionBase = | 'off'
    | /** @deprecated use `'readonly'` */ 'readable'
    | 'readonly'
    | 'writable'
    | /** @deprecated use `'writable'` */ 'writeable';
```

### `GlobalVariableOptionBoolean`

```ts
type GlobalVariableOptionBoolean = | /** @deprecated use `'readonly'` */ false
    | /** @deprecated use `'writable'` */ true;
```

### `GlobalVariableOption`

```ts
type GlobalVariableOption = | GlobalVariableOptionBase
    | GlobalVariableOptionBoolean;
```

### `ParserOptions`

```ts
type ParserOptions = ParserOptionsTypes.ParserOptions;
```

### `EnvironmentConfig`

```ts
type EnvironmentConfig = SharedConfig.EnvironmentConfig;
```

### `GlobalsConfig`

```ts
type GlobalsConfig = SharedConfig.GlobalsConfig;
```

### `GlobalVariableOption`

```ts
type GlobalVariableOption = SharedConfig.GlobalVariableOption;
```

### `GlobalVariableOptionBase`

```ts
type GlobalVariableOptionBase = SharedConfig.GlobalVariableOptionBase;
```

### `ParserOptions`

```ts
type ParserOptions = SharedConfig.ParserOptions;
```

### `RuleEntry`

```ts
type RuleEntry = SharedConfig.RuleEntry;
```

### `RuleLevel`

```ts
type RuleLevel = SharedConfig.RuleLevel;
```

### `RuleLevelAndOptions`

```ts
type RuleLevelAndOptions = SharedConfig.RuleLevelAndOptions;
```

### `RulesRecord`

```ts
type RulesRecord = SharedConfig.RulesRecord;
```

### `Severity`

```ts
type Severity = SharedConfig.Severity;
```

### `SeverityString`

```ts
type SeverityString = SharedConfig.SeverityString;
```

### `EcmaVersion`

```ts
type EcmaVersion = ParserOptionsTypes.EcmaVersion;
```

### `GlobalsConfig`

```ts
type GlobalsConfig = SharedConfig.GlobalsConfig;
```

### `Parser`

```ts
type Parser = ParserType.LooseParserModule;
```

### `ParserOptions`

```ts
type ParserOptions = SharedConfig.ParserOptions;
```

### `PluginMeta`

```ts
type PluginMeta = SharedConfig.PluginMeta;
```

### `Processor`

```ts
type Processor = ProcessorType.LooseProcessorModule;
```

### `RuleEntry`

```ts
type RuleEntry = SharedConfig.RuleEntry;
```

### `RuleLevel`

```ts
type RuleLevel = SharedConfig.RuleLevel;
```

### `RuleLevelAndOptions`

```ts
type RuleLevelAndOptions = SharedConfig.RuleLevelAndOptions;
```

### `Rules`

```ts
type Rules = SharedConfig.RulesRecord;
```

### `Settings`

```ts
type Settings = SharedConfigurationSettings;
```

### `Severity`

```ts
type Severity = SharedConfig.Severity;
```

### `SeverityString`

```ts
type SeverityString = SharedConfig.SeverityString;
```

### `SourceType`

```ts
type SourceType = 'commonjs' | ParserOptionsTypes.SourceType;
```

### `ConfigArray`

```ts
type ConfigArray = Config[];
```

### `ConfigPromise`

```ts
type ConfigPromise = Promise<ConfigArray>;
```

### `ConfigFile`

```ts
type ConfigFile = ConfigArray | ConfigPromise;
```


---