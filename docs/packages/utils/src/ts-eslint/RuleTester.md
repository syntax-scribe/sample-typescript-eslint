[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `RuleTester.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 2
- **Imports**: 10
- **Interfaces**: 6
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/utils/src/ts-eslint/RuleTester.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintRuleTester` | `eslint` |
| `AST_NODE_TYPES` | `../ts-estree` |
| `AST_TOKEN_TYPES` | `../ts-estree` |
| `ClassicConfig` | `./Config` |
| `Linter` | `./Linter` |
| `ParserOptions` | `./ParserOptions` |
| `ReportDescriptorMessageData` | `./Rule` |
| `RuleCreateFunction` | `./Rule` |
| `RuleModule` | `./Rule` |
| `SharedConfigurationSettings` | `./Rule` |


---

## Functions

### `RuleTesterBase.run(ruleName: string, rule: RuleModule<MessageIds, Options>, tests: RunTests<MessageIds, Options>): void`

<details><summary>Code</summary>

```ts
run<MessageIds extends string, Options extends readonly unknown[]>(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    tests: RunTests<MessageIds, Options>,
  ): void;
```
</details>

- **JSDoc**:
```ts
/**
   * Adds a new rule test to execute.
   * @param ruleName The name of the rule to run.
   * @param rule The rule to test.
   * @param tests The collection of tests to run.
   */
```

- **Parameters**:
  - `ruleName: string`
  - `rule: RuleModule<MessageIds, Options>`
  - `tests: RunTests<MessageIds, Options>`
- **Return Type**: `void`
### `RuleTesterBase.defineRule(name: string, rule: | RuleCreateFunction<MessageIds, Options>
      | RuleModule<MessageIds, Options>): void`

<details><summary>Code</summary>

```ts
defineRule<MessageIds extends string, Options extends readonly unknown[]>(
    name: string,
    rule:
      | RuleCreateFunction<MessageIds, Options>
      | RuleModule<MessageIds, Options>,
  ): void;
```
</details>

- **JSDoc**:
```ts
/**
   * Define a rule for one particular run of tests.
   */
```

- **Parameters**:
  - `name: string`
  - `rule: | RuleCreateFunction<MessageIds, Options>
      | RuleModule<MessageIds, Options>`
- **Return Type**: `void`

---

## Classes

### `RuleTesterBase`

<details><summary>Class Code</summary>

```ts
declare class RuleTesterBase {
  /**
   * Creates a new instance of RuleTester.
   * @param testerConfig extra configuration for the tester
   */
  constructor(testerConfig?: RuleTesterConfig);

  /**
   * Adds a new rule test to execute.
   * @param ruleName The name of the rule to run.
   * @param rule The rule to test.
   * @param tests The collection of tests to run.
   */
  run<MessageIds extends string, Options extends readonly unknown[]>(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    tests: RunTests<MessageIds, Options>,
  ): void;

  /**
   * If you supply a value to this property, the rule tester will call this instead of using the version defined on
   * the global namespace.
   */
  static get describe(): RuleTesterTestFrameworkFunction;
  static set describe(value: RuleTesterTestFrameworkFunction | undefined);

  /**
   * If you supply a value to this property, the rule tester will call this instead of using the version defined on
   * the global namespace.
   */
  static get it(): RuleTesterTestFrameworkFunction;
  static set it(value: RuleTesterTestFrameworkFunction | undefined);

  /**
   * If you supply a value to this property, the rule tester will call this instead of using the version defined on
   * the global namespace.
   */
  static get itOnly(): RuleTesterTestFrameworkFunction;
  static set itOnly(value: RuleTesterTestFrameworkFunction | undefined);

  /**
   * Define a rule for one particular run of tests.
   */
  defineRule<MessageIds extends string, Options extends readonly unknown[]>(
    name: string,
    rule:
      | RuleCreateFunction<MessageIds, Options>
      | RuleModule<MessageIds, Options>,
  ): void;
}
```
</details>

#### Methods

##### `run(ruleName: string, rule: RuleModule<MessageIds, Options>, tests: RunTests<MessageIds, Options>): void`

<details><summary>Code</summary>

```ts
run<MessageIds extends string, Options extends readonly unknown[]>(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    tests: RunTests<MessageIds, Options>,
  ): void;
```
</details>

##### `defineRule(name: string, rule: | RuleCreateFunction<MessageIds, Options>
      | RuleModule<MessageIds, Options>): void`

<details><summary>Code</summary>

```ts
defineRule<MessageIds extends string, Options extends readonly unknown[]>(
    name: string,
    rule:
      | RuleCreateFunction<MessageIds, Options>
      | RuleModule<MessageIds, Options>,
  ): void;
```
</details>

### `RuleTester`

<details><summary>Class Code</summary>

```ts
export class RuleTester extends (ESLintRuleTester as typeof RuleTesterBase) {}
```
</details>


---

## Interfaces

### `ValidTestCase<Options extends readonly unknown[]>`

<details><summary>Interface Code</summary>

```ts
export interface ValidTestCase<Options extends readonly unknown[]> {
  /**
   * Code for the test case.
   */
  readonly code: string;
  /**
   * Environments for the test case.
   */
  readonly env?: Readonly<Linter.EnvironmentConfig>;
  /**
   * The fake filename for the test case. Useful for rules that make assertion about filenames.
   */
  readonly filename?: string;
  /**
   * The additional global variables.
   */
  readonly globals?: Readonly<Linter.GlobalsConfig>;
  /**
   * Name for the test case.
   */
  readonly name?: string;
  /**
   * Run this case exclusively for debugging in supported test frameworks.
   */
  readonly only?: boolean;
  /**
   * Options for the test case.
   */
  readonly options?: Readonly<Options>;
  /**
   * The absolute path for the parser.
   */
  readonly parser?: string;
  /**
   * Options for the parser.
   */
  readonly parserOptions?: Readonly<ParserOptions>;
  /**
   * Settings for the test case.
   */
  readonly settings?: Readonly<SharedConfigurationSettings>;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `code` | `string` | ✗ |  |
| `env` | `Readonly<Linter.EnvironmentConfig>` | ✓ |  |
| `filename` | `string` | ✓ |  |
| `globals` | `Readonly<Linter.GlobalsConfig>` | ✓ |  |
| `name` | `string` | ✓ |  |
| `only` | `boolean` | ✓ |  |
| `options` | `Readonly<Options>` | ✓ |  |
| `parser` | `string` | ✓ |  |
| `parserOptions` | `Readonly<ParserOptions>` | ✓ |  |
| `settings` | `Readonly<SharedConfigurationSettings>` | ✓ |  |

### `SuggestionOutput<MessageIds extends string>`

<details><summary>Interface Code</summary>

```ts
export interface SuggestionOutput<MessageIds extends string> {
  /**
   * The data used to fill the message template.
   */
  readonly data?: ReportDescriptorMessageData;
  /**
   * Reported message ID.
   */
  readonly messageId: MessageIds;
  /**
   * NOTE: Suggestions will be applied as a stand-alone change, without triggering multi-pass fixes.
   * Each individual error has its own suggestion, so you have to show the correct, _isolated_ output for each suggestion.
   */
  readonly output: string;

  // we disallow this because it's much better to use messageIds for reusable errors that are easily testable
  // readonly desc?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `data` | `ReportDescriptorMessageData` | ✓ |  |
| `messageId` | `MessageIds` | ✗ |  |
| `output` | `string` | ✗ |  |

### `InvalidTestCase<MessageIds extends string, Options extends readonly unknown[]>`

<details><summary>Interface Code</summary>

```ts
export interface InvalidTestCase<
  MessageIds extends string,
  Options extends readonly unknown[],
> extends ValidTestCase<Options> {
  /**
   * Expected errors.
   */
  readonly errors: readonly TestCaseError<MessageIds>[];
  /**
   * The expected code after autofixes are applied. If set to `null`, the test runner will assert that no autofix is suggested.
   */
  readonly output?: string | string[] | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `errors` | `readonly TestCaseError<MessageIds>[]` | ✗ |  |
| `output` | `string | string[] | null` | ✓ |  |

### `TestCaseError<MessageIds extends string>`

<details><summary>Interface Code</summary>

```ts
export interface TestCaseError<MessageIds extends string> {
  /**
   * The 1-based column number of the reported start location.
   */
  readonly column?: number;
  /**
   * The data used to fill the message template.
   */
  readonly data?: ReportDescriptorMessageData;
  /**
   * The 1-based column number of the reported end location.
   */
  readonly endColumn?: number;
  /**
   * The 1-based line number of the reported end location.
   */
  readonly endLine?: number;
  /**
   * The 1-based line number of the reported start location.
   */
  readonly line?: number;
  /**
   * Reported message ID.
   */
  readonly messageId: MessageIds;
  /**
   * Reported suggestions.
   */
  readonly suggestions?: readonly SuggestionOutput<MessageIds>[] | null;
  /**
   * The type of the reported AST node.
   */
  readonly type?: AST_NODE_TYPES | AST_TOKEN_TYPES;

  // we disallow this because it's much better to use messageIds for reusable errors that are easily testable
  // readonly message?: string | RegExp;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `column` | `number` | ✓ |  |
| `data` | `ReportDescriptorMessageData` | ✓ |  |
| `endColumn` | `number` | ✓ |  |
| `endLine` | `number` | ✓ |  |
| `line` | `number` | ✓ |  |
| `messageId` | `MessageIds` | ✗ |  |
| `suggestions` | `readonly SuggestionOutput<MessageIds>[] | null` | ✓ |  |
| `type` | `AST_NODE_TYPES | AST_TOKEN_TYPES` | ✓ |  |

### `RunTests<MessageIds extends string, Options extends readonly unknown[]>`

<details><summary>Interface Code</summary>

```ts
export interface RunTests<
  MessageIds extends string,
  Options extends readonly unknown[],
> {
  // RuleTester.run also accepts strings for valid cases
  readonly invalid: readonly InvalidTestCase<MessageIds, Options>[];
  readonly valid: readonly (string | ValidTestCase<Options>)[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `invalid` | `readonly InvalidTestCase<MessageIds, Options>[]` | ✗ |  |
| `valid` | `readonly (string | ValidTestCase<Options>)[]` | ✗ |  |

### `RuleTesterConfig`

<details><summary>Interface Code</summary>

```ts
export interface RuleTesterConfig extends ClassicConfig.Config {
  // should be require.resolve(parserPackageName)
  readonly parser: string;
  readonly parserOptions?: Readonly<ParserOptions>;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parser` | `string` | ✗ |  |
| `parserOptions` | `Readonly<ParserOptions>` | ✓ |  |


---

## Type Aliases

### `RuleTesterTestFrameworkFunction`

/**
 * @param text a string describing the rule
 * @deprecated Use `@typescript-eslint/rule-tester` instead.
 */

```ts
type RuleTesterTestFrameworkFunction = (
  text: string,
  callback: () => void,
) => void;
```


---