[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ValidTestCase.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 2
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-tester/src/types/ValidTestCase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Linter` | `@typescript-eslint/utils/ts-eslint` |
| `Parser` | `@typescript-eslint/utils/ts-eslint` |
| `ParserOptions` | `@typescript-eslint/utils/ts-eslint` |
| `SharedConfigurationSettings` | `@typescript-eslint/utils/ts-eslint` |
| `DependencyConstraint` | `./DependencyConstraint` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TestLanguageOptions`

<details><summary>Interface Code</summary>

```ts
export interface TestLanguageOptions {
  /**
   * Environments for the test case.
   */
  readonly env?: Readonly<Linter.EnvironmentConfig>;
  /**
   * The additional global variables.
   */
  readonly globals?: Readonly<Linter.GlobalsConfig>;
  /**
   * The absolute path for the parser.
   */
  readonly parser?: Readonly<Parser.LooseParserModule>;
  /**
   * Options for the parser.
   */
  readonly parserOptions?: Readonly<ParserOptions>;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `env` | `Readonly<Linter.EnvironmentConfig>` | ✓ |  |
| `globals` | `Readonly<Linter.GlobalsConfig>` | ✓ |  |
| `parser` | `Readonly<Parser.LooseParserModule>` | ✓ |  |
| `parserOptions` | `Readonly<ParserOptions>` | ✓ |  |

### `ValidTestCase<Options extends readonly unknown[]>`

<details><summary>Interface Code</summary>

```ts
export interface ValidTestCase<Options extends readonly unknown[]> {
  /**
   * Function to execute after testing the case regardless of its result.
   */
  readonly after?: () => void;
  /**
   * Function to execute before testing the case.
   */
  readonly before?: () => void;
  /**
   * Code for the test case.
   */
  readonly code: string;
  /**
   * Constraints that must pass in the current environment for the test to run
   */
  readonly dependencyConstraints?: DependencyConstraint;
  /**
   * The fake filename for the test case. Useful for rules that make assertion about filenames.
   */
  readonly filename?: string;
  /**
   * Language options for the test case.
   */
  readonly languageOptions?: TestLanguageOptions;
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
   * Settings for the test case.
   */
  readonly settings?: Readonly<SharedConfigurationSettings>;
  /**
   * Skip this case in supported test frameworks.
   */
  readonly skip?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `after` | `() => void` | ✓ |  |
| `before` | `() => void` | ✓ |  |
| `code` | `string` | ✗ |  |
| `dependencyConstraints` | `DependencyConstraint` | ✓ |  |
| `filename` | `string` | ✓ |  |
| `languageOptions` | `TestLanguageOptions` | ✓ |  |
| `name` | `string` | ✓ |  |
| `only` | `boolean` | ✓ |  |
| `options` | `Readonly<Options>` | ✓ |  |
| `settings` | `Readonly<SharedConfigurationSettings>` | ✓ |  |
| `skip` | `boolean` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---