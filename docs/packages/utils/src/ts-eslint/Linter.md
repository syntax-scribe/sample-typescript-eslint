[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Linter.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 7 |
| 🧱 Classes | 2 |
| 📦 Imports | 12 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 8 |
| 📑 Type Aliases | 22 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/utils/src/ts-eslint/Linter.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintLinter` | `eslint` |
| `ClassicConfig` | `./Config` |
| `FlatConfig` | `./Config` |
| `SharedConfig` | `./Config` |
| `Parser` | `./Parser` |
| `ProcessorType` | `./Processor` |
| `AnyRuleCreateFunction` | `./Rule` |
| `AnyRuleModule` | `./Rule` |
| `RuleCreateFunction` | `./Rule` |
| `RuleFix` | `./Rule` |
| `RuleModule` | `./Rule` |
| `SourceCode` | `./SourceCode` |


---

## Functions

### `LinterBase.defineParser(parserId: string, parserModule: Parser.LooseParserModule): void`

<details><summary>Code</summary>

```ts
defineParser(parserId: string, parserModule: Parser.LooseParserModule): void;
```
</details>

- **JSDoc**:
```ts
/**
   * Define a new parser module
   * @param parserId Name of the parser
   * @param parserModule The parser object
   */
```

- **Parameters**:
  - `parserId: string`
  - `parserModule: Parser.LooseParserModule`
- **Return Type**: `void`
### `LinterBase.defineRule(ruleId: string, ruleModule: MinimalRuleModule<MessageIds, Options> | RuleCreateFunction): void`

<details><summary>Code</summary>

```ts
defineRule<MessageIds extends string, Options extends readonly unknown[]>(
    ruleId: string,
    ruleModule: MinimalRuleModule<MessageIds, Options> | RuleCreateFunction,
  ): void;
```
</details>

- **JSDoc**:
```ts
/**
   * Defines a new linting rule.
   * @param ruleId A unique rule identifier
   * @param ruleModule Function from context to object mapping AST node types to event handlers
   */
```

- **Parameters**:
  - `ruleId: string`
  - `ruleModule: MinimalRuleModule<MessageIds, Options> | RuleCreateFunction`
- **Return Type**: `void`
### `LinterBase.defineRules(rulesToDefine: Record<
      string,
      | MinimalRuleModule<MessageIds, Options>
      | RuleCreateFunction<MessageIds, Options>
    >): void`

<details><summary>Code</summary>

```ts
defineRules<MessageIds extends string, Options extends readonly unknown[]>(
    rulesToDefine: Record<
      string,
      | MinimalRuleModule<MessageIds, Options>
      | RuleCreateFunction<MessageIds, Options>
    >,
  ): void;
```
</details>

- **JSDoc**:
```ts
/**
   * Defines many new linting rules.
   * @param rulesToDefine map from unique rule identifier to rule
   */
```

- **Parameters**:
  - `rulesToDefine: Record<
      string,
      | MinimalRuleModule<MessageIds, Options>
      | RuleCreateFunction<MessageIds, Options>
    >`
- **Return Type**: `void`
### `LinterBase.getRules(): Map<string, MinimalRuleModule<string, unknown[]>>`

<details><summary>Code</summary>

```ts
getRules(): Map<string, MinimalRuleModule<string, unknown[]>>;
```
</details>

- **JSDoc**:
```ts
/**
   * Gets an object with all loaded rules.
   * @returns All loaded rules
   */
```

- **Return Type**: `Map<string, MinimalRuleModule<string, unknown[]>>`
### `LinterBase.getSourceCode(): SourceCode`

<details><summary>Code</summary>

```ts
getSourceCode(): SourceCode;
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the `SourceCode` object representing the parsed source.
   * @returns The `SourceCode` object.
   */
```

- **Return Type**: `SourceCode`
### `LinterBase.verify(textOrSourceCode: string | SourceCode, config: Linter.ConfigType, filenameOrOptions: string | Linter.VerifyOptions): Linter.LintMessage[]`

<details><summary>Code</summary>

```ts
verify(
    textOrSourceCode: string | SourceCode,
    config: Linter.ConfigType,
    filenameOrOptions?: string | Linter.VerifyOptions,
  ): Linter.LintMessage[];
```
</details>

- **JSDoc**:
```ts
/**
   * Verifies the text against the rules specified by the second argument.
   * @param textOrSourceCode The text to parse or a SourceCode object.
   * @param config An ESLintConfig instance to configure everything.
   * @param filenameOrOptions The optional filename of the file being checked.
   *        If this is not set, the filename will default to '<input>' in the rule context.
   *        If this is an object, then it has "filename", "allowInlineConfig", and some properties.
   * @returns The results as an array of messages or an empty array if no messages.
   */
```

- **Parameters**:
  - `textOrSourceCode: string | SourceCode`
  - `config: Linter.ConfigType`
  - `filenameOrOptions: string | Linter.VerifyOptions`
- **Return Type**: `Linter.LintMessage[]`
### `LinterBase.verifyAndFix(code: string, config: Linter.ConfigType, options: Linter.FixOptions): Linter.FixReport`

<details><summary>Code</summary>

```ts
verifyAndFix(
    code: string,
    config: Linter.ConfigType,
    options: Linter.FixOptions,
  ): Linter.FixReport;
```
</details>

- **JSDoc**:
```ts
/**
   * Performs multiple autofix passes over the text until as many fixes as possible have been applied.
   * @param code The source text to apply fixes to.
   * @param config The ESLint config object to use.
   * @param options The ESLint options object to use.
   * @returns The result of the fix operation as returned from the SourceCodeFixer.
   */
```

- **Parameters**:
  - `code: string`
  - `config: Linter.ConfigType`
  - `options: Linter.FixOptions`
- **Return Type**: `Linter.FixReport`

---

## Classes

### `LinterBase`

<details><summary>Class Code</summary>

```ts
declare class LinterBase {
  /**
   * The version from package.json.
   */
  readonly version: string;

  /**
   * Initialize the Linter.
   * @param config the config object
   */
  constructor(config?: Linter.LinterOptions);

  /**
   * Define a new parser module
   * @param parserId Name of the parser
   * @param parserModule The parser object
   */
  defineParser(parserId: string, parserModule: Parser.LooseParserModule): void;

  /**
   * Defines a new linting rule.
   * @param ruleId A unique rule identifier
   * @param ruleModule Function from context to object mapping AST node types to event handlers
   */
  defineRule<MessageIds extends string, Options extends readonly unknown[]>(
    ruleId: string,
    ruleModule: MinimalRuleModule<MessageIds, Options> | RuleCreateFunction,
  ): void;

  /**
   * Defines many new linting rules.
   * @param rulesToDefine map from unique rule identifier to rule
   */
  defineRules<MessageIds extends string, Options extends readonly unknown[]>(
    rulesToDefine: Record<
      string,
      | MinimalRuleModule<MessageIds, Options>
      | RuleCreateFunction<MessageIds, Options>
    >,
  ): void;

  /**
   * Gets an object with all loaded rules.
   * @returns All loaded rules
   */
  getRules(): Map<string, MinimalRuleModule<string, unknown[]>>;

  /**
   * Gets the `SourceCode` object representing the parsed source.
   * @returns The `SourceCode` object.
   */
  getSourceCode(): SourceCode;

  /**
   * Verifies the text against the rules specified by the second argument.
   * @param textOrSourceCode The text to parse or a SourceCode object.
   * @param config An ESLintConfig instance to configure everything.
   * @param filenameOrOptions The optional filename of the file being checked.
   *        If this is not set, the filename will default to '<input>' in the rule context.
   *        If this is an object, then it has "filename", "allowInlineConfig", and some properties.
   * @returns The results as an array of messages or an empty array if no messages.
   */
  verify(
    textOrSourceCode: string | SourceCode,
    config: Linter.ConfigType,
    filenameOrOptions?: string | Linter.VerifyOptions,
  ): Linter.LintMessage[];

  ////////////////////
  // static members //
  ////////////////////

  /**
   * The version from package.json.
   */
  static readonly version: string;

  /**
   * Performs multiple autofix passes over the text until as many fixes as possible have been applied.
   * @param code The source text to apply fixes to.
   * @param config The ESLint config object to use.
   * @param options The ESLint options object to use.
   * @returns The result of the fix operation as returned from the SourceCodeFixer.
   */
  verifyAndFix(
    code: string,
    config: Linter.ConfigType,
    options: Linter.FixOptions,
  ): Linter.FixReport;
}
```
</details>

#### Methods

##### `defineParser(parserId: string, parserModule: Parser.LooseParserModule): void`

<details><summary>Code</summary>

```ts
defineParser(parserId: string, parserModule: Parser.LooseParserModule): void;
```
</details>

##### `defineRule(ruleId: string, ruleModule: MinimalRuleModule<MessageIds, Options> | RuleCreateFunction): void`

<details><summary>Code</summary>

```ts
defineRule<MessageIds extends string, Options extends readonly unknown[]>(
    ruleId: string,
    ruleModule: MinimalRuleModule<MessageIds, Options> | RuleCreateFunction,
  ): void;
```
</details>

##### `defineRules(rulesToDefine: Record<
      string,
      | MinimalRuleModule<MessageIds, Options>
      | RuleCreateFunction<MessageIds, Options>
    >): void`

<details><summary>Code</summary>

```ts
defineRules<MessageIds extends string, Options extends readonly unknown[]>(
    rulesToDefine: Record<
      string,
      | MinimalRuleModule<MessageIds, Options>
      | RuleCreateFunction<MessageIds, Options>
    >,
  ): void;
```
</details>

##### `getRules(): Map<string, MinimalRuleModule<string, unknown[]>>`

<details><summary>Code</summary>

```ts
getRules(): Map<string, MinimalRuleModule<string, unknown[]>>;
```
</details>

##### `getSourceCode(): SourceCode`

<details><summary>Code</summary>

```ts
getSourceCode(): SourceCode;
```
</details>

##### `verify(textOrSourceCode: string | SourceCode, config: Linter.ConfigType, filenameOrOptions: string | Linter.VerifyOptions): Linter.LintMessage[]`

<details><summary>Code</summary>

```ts
verify(
    textOrSourceCode: string | SourceCode,
    config: Linter.ConfigType,
    filenameOrOptions?: string | Linter.VerifyOptions,
  ): Linter.LintMessage[];
```
</details>

##### `verifyAndFix(code: string, config: Linter.ConfigType, options: Linter.FixOptions): Linter.FixReport`

<details><summary>Code</summary>

```ts
verifyAndFix(
    code: string,
    config: Linter.ConfigType,
    options: Linter.FixOptions,
  ): Linter.FixReport;
```
</details>

### `Linter`

<details><summary>Class Code</summary>

```ts
class Linter extends (ESLintLinter as typeof LinterBase) {}
```
</details>


---

## Interfaces

### `LinterOptions`

<details><summary>Interface Code</summary>

```ts
export interface LinterOptions {
    /**
     * Which config format to use.
     * @default 'flat'
     */
    configType?: ConfigTypeSpecifier;

    /**
     * path to a directory that should be considered as the current working directory.
     */
    cwd?: string;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `configType` | `ConfigTypeSpecifier` | ✓ |  |
| `cwd` | `string` | ✓ |  |

### `VerifyOptions`

<details><summary>Interface Code</summary>

```ts
export interface VerifyOptions {
    /**
     * Allow/disallow inline comments' ability to change config once it is set. Defaults to true if not supplied.
     * Useful if you want to validate JS without comments overriding rules.
     */
    allowInlineConfig?: boolean;
    /**
     * if `true` then the linter doesn't make `fix` properties into the lint result.
     */
    disableFixes?: boolean;
    /**
     * the filename of the source code.
     */
    filename?: string;
    /**
     * the predicate function that selects adopt code blocks.
     */
    filterCodeBlock?: (filename: string, text: string) => boolean;
    /**
     * postprocessor for report messages.
     * If provided, this should accept an array of the message lists
     * for each code block returned from the preprocessor, apply a mapping to
     * the messages as appropriate, and return a one-dimensional array of
     * messages.
     */
    postprocess?: ProcessorType.PostProcess;
    /**
     * preprocessor for source text.
     * If provided, this should accept a string of source text, and return an array of code blocks to lint.
     */
    preprocess?: ProcessorType.PreProcess;
    /**
     * Adds reported errors for unused `eslint-disable` directives.
     */
    reportUnusedDisableDirectives?: boolean | SeverityString;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `allowInlineConfig` | `boolean` | ✓ |  |
| `disableFixes` | `boolean` | ✓ |  |
| `filename` | `string` | ✓ |  |
| `filterCodeBlock` | `(filename: string, text: string) => boolean` | ✓ |  |
| `postprocess` | `ProcessorType.PostProcess` | ✓ |  |
| `preprocess` | `ProcessorType.PreProcess` | ✓ |  |
| `reportUnusedDisableDirectives` | `boolean | SeverityString` | ✓ |  |

### `FixOptions`

<details><summary>Interface Code</summary>

```ts
export interface FixOptions extends VerifyOptions {
    /**
     * Determines whether fixes should be applied.
     */
    fix?: boolean;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `fix` | `boolean` | ✓ |  |

### `LintSuggestion`

<details><summary>Interface Code</summary>

```ts
export interface LintSuggestion {
    desc: string;
    fix: RuleFix;
    messageId?: string;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `desc` | `string` | ✗ |  |
| `fix` | `RuleFix` | ✗ |  |
| `messageId` | `string` | ✓ |  |

### `LintMessage`

<details><summary>Interface Code</summary>

```ts
export interface LintMessage {
    /**
     * The 1-based column number.
     */
    column: number;
    /**
     * The 1-based column number of the end location.
     */
    endColumn?: number;
    /**
     * The 1-based line number of the end location.
     */
    endLine?: number;
    /**
     * If `true` then this is a fatal error.
     */
    fatal?: true;
    /**
     * Information for autofix.
     */
    fix?: RuleFix;
    /**
     * The 1-based line number.
     */
    line: number;
    /**
     * The error message.
     */
    message: string;
    messageId?: string;
    nodeType: string;
    /**
     * The ID of the rule which makes this message.
     */
    ruleId: string | null;
    /**
     * The severity of this message.
     */
    severity: Severity;
    source: string | null;
    /**
     * Information for suggestions
     */
    suggestions?: LintSuggestion[];
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `column` | `number` | ✗ |  |
| `endColumn` | `number` | ✓ |  |
| `endLine` | `number` | ✓ |  |
| `fatal` | `true` | ✓ |  |
| `fix` | `RuleFix` | ✓ |  |
| `line` | `number` | ✗ |  |
| `message` | `string` | ✗ |  |
| `messageId` | `string` | ✓ |  |
| `nodeType` | `string` | ✗ |  |
| `ruleId` | `string | null` | ✗ |  |
| `severity` | `Severity` | ✗ |  |
| `source` | `string | null` | ✗ |  |
| `suggestions` | `LintSuggestion[]` | ✓ |  |

### `FixReport`

<details><summary>Interface Code</summary>

```ts
export interface FixReport {
    /**
     * True, if the code was fixed
     */
    fixed: boolean;
    /**
     * Collection of all messages for the given code
     */
    messages: LintMessage[];
    /**
     * Fixed code text (might be the same as input if no fixes were applied).
     */
    output: string;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `fixed` | `boolean` | ✗ |  |
| `messages` | `LintMessage[]` | ✗ |  |
| `output` | `string` | ✗ |  |

### `Environment`

<details><summary>Interface Code</summary>

```ts
export interface Environment {
    /**
     * The definition of global variables.
     */
    globals?: GlobalsConfig;
    /**
     * The parser options that will be enabled under this environment.
     */
    parserOptions?: ParserOptions;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `globals` | `GlobalsConfig` | ✓ |  |
| `parserOptions` | `ParserOptions` | ✓ |  |

### `Plugin`

<details><summary>Interface Code</summary>

```ts
export interface Plugin {
    /**
     * The definition of plugin configs.
     */
    configs?: Record<string, ClassicConfig.Config>;
    /**
     * The definition of plugin environments.
     */
    environments?: Record<string, Environment>;
    /**
     * Metadata about your plugin for easier debugging and more effective caching of plugins.
     */
    meta?: PluginMeta;
    /**
     * The definition of plugin processors.
     */
    processors?: Record<string, ProcessorType.ProcessorModule>;
    /**
     * The definition of plugin rules.
     */
    rules?: LegacyPluginRules;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `configs` | `Record<string, ClassicConfig.Config>` | ✓ |  |
| `environments` | `Record<string, Environment>` | ✓ |  |
| `meta` | `PluginMeta` | ✓ |  |
| `processors` | `Record<string, ProcessorType.ProcessorModule>` | ✓ |  |
| `rules` | `LegacyPluginRules` | ✓ |  |


---

## Type Aliases

### `MinimalRuleModule<MessageIds extends string = string extends string = string, Options extends readonly unknown[] = [] extends readonly unknown[] = []>`

```ts
type MinimalRuleModule<MessageIds extends string = string extends string = string, Options extends readonly unknown[] = [] extends readonly unknown[] = []> = Partial<Omit<RuleModule<MessageIds, Options>, 'create'>> &
  Pick<RuleModule<MessageIds, Options>, 'create'>;
```

### `ConfigTypeSpecifier`

```ts
type ConfigTypeSpecifier = 'eslintrc' | 'flat';
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

### `PluginMeta`

```ts
type PluginMeta = SharedConfig.PluginMeta;
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

### `Config`

/** @deprecated use {@link Linter.ConfigType} instead */

```ts
type Config = ClassicConfig.Config;
```

### `ConfigType`

```ts
type ConfigType = | ClassicConfig.Config
    | FlatConfig.Config
    | FlatConfig.ConfigArray;
```

### `ConfigOverride`

/** @deprecated use {@link ClassicConfig.ConfigOverride} instead */

```ts
type ConfigOverride = ClassicConfig.ConfigOverride;
```

### `ParserModule`

/** @deprecated use {@link Parser.ParserModule} */

```ts
type ParserModule = Parser.LooseParserModule;
```

### `ESLintParseResult`

/** @deprecated use {@link Parser.ParseResult} */

```ts
type ESLintParseResult = Parser.ParseResult;
```

### `Processor`

/** @deprecated use {@link ProcessorType.ProcessorModule} */

```ts
type Processor = ProcessorType.ProcessorModule;
```

### `LegacyPluginRules`

```ts
type LegacyPluginRules = Record<
    string,
    AnyRuleCreateFunction | AnyRuleModule
  >;
```

### `PluginRules`

```ts
type PluginRules = Record<string, AnyRuleModule>;
```


---