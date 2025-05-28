[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `RuleTester.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 24 |
| 🧱 Classes | 1 |
| 📦 Imports | 42 |
| 📊 Variables & Constants | 52 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Classes](#classes)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/RuleTester.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `TSUtils` | `@typescript-eslint/utils` |
| `AnyRuleCreateFunction` | `@typescript-eslint/utils/ts-eslint` |
| `AnyRuleModule` | `@typescript-eslint/utils/ts-eslint` |
| `ParserOptions` | `@typescript-eslint/utils/ts-eslint` |
| `RuleListener` | `@typescript-eslint/utils/ts-eslint` |
| `RuleModule` | `@typescript-eslint/utils/ts-eslint` |
| `deepMerge` | `@typescript-eslint/utils/eslint-utils` |
| `Linter` | `@typescript-eslint/utils/ts-eslint` |
| `assert` | `node:assert` |
| `path` | `node:path` |
| `util` | `node:util` |
| `SourceCode` | `eslint` |
| `stringify` | `json-stable-stringify-without-jsonify` |
| `merge` | `lodash.merge` |
| `InvalidTestCase` | `./types` |
| `NormalizedRunTests` | `./types` |
| `RuleTesterConfig` | `./types` |
| `RunTests` | `./types` |
| `SuggestionOutput` | `./types` |
| `TesterConfigWithDefaults` | `./types` |
| `ValidTestCase` | `./types` |
| `TestFramework` | `./TestFramework` |
| `ajvBuilder` | `./utils/ajv` |
| `cloneDeeplyExcludesParent` | `./utils/cloneDeeplyExcludesParent` |
| `validate` | `./utils/config-validator` |
| `satisfiesAllDependencyConstraints` | `./utils/dependencyConstraints` |
| `freezeDeeply` | `./utils/freezeDeeply` |
| `getRuleOptionsSchema` | `./utils/getRuleOptionsSchema` |
| `hasOwnProperty` | `./utils/hasOwnProperty` |
| `getPlaceholderMatcher` | `./utils/interpolate` |
| `interpolate` | `./utils/interpolate` |
| `omitCustomConfigProperties` | `./utils/omitCustomConfigProperties` |
| `isSerializable` | `./utils/serialization` |
| `ERROR_OBJECT_PARAMETERS` | `./utils/validationHelpers` |
| `FRIENDLY_ERROR_OBJECT_PARAMETER_LIST` | `./utils/validationHelpers` |
| `FRIENDLY_SUGGESTION_OBJECT_PARAMETER_LIST` | `./utils/validationHelpers` |
| `REQUIRED_SCENARIOS` | `./utils/validationHelpers` |
| `RULE_TESTER_PARAMETERS` | `./utils/validationHelpers` |
| `sanitize` | `./utils/validationHelpers` |
| `SUGGESTION_OBJECT_PARAMETERS` | `./utils/validationHelpers` |
| `wrapParser` | `./utils/validationHelpers` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `RULE_TESTER_PLUGIN` | `"@rule-tester"` | const | `'@rule-tester'` | ✗ |
| `RULE_TESTER_PLUGIN_PREFIX` | `"@rule-tester/"` | const | ``${RULE_TESTER_PLUGIN}/`` | ✗ |
| `TYPESCRIPT_ESLINT_PARSER` | `"@typescript-eslint/parser"` | const | `'@typescript-eslint/parser'` | ✗ |
| `DUPLICATE_PARSER_ERROR_MESSAGE` | `"Do not set the parser at the test level unless you want to use a parser other than \"@typescript-eslint/parser\""` | const | ``Do not set the parser at the test level unless you want to use a parser other than "${TYPESCRIPT_ESLINT_PARSER}"`` | ✗ |
| `defaultParser` | `any` | const | `require(TYPESCRIPT_ESLINT_PARSER) as typeof ParserType` | ✗ |
| `testerDefaultConfig` | `Readonly<TesterConfigWithDefaults>` | const | `{
  defaultFilenames: { ts: 'file.ts', tsx: 'react.tsx' },
  languageOptions: {
    parser: defaultParser,
  },
  rules: {},
}` | ✗ |
| `defaultConfig` | `Mutable<Required<Pick<RuleTesterConfig, "defaultFilenames" | "languageOptions" | "rules">> & RuleTesterConfig>` | let/var | `deepMerge(
  {},
  testerDefaultConfig,
) as TesterConfigWithDefaults` | ✗ |
| `forbiddenMethods` | `readonly ["applyInlineConfig", "applyLanguageOptions", "finalize"]` | const | `[
  'applyInlineConfig',
  'applyLanguageOptions',
  'finalize',
] as const` | ✗ |
| `forbiddenMethodCalls` | `Map<"applyInlineConfig" | "applyLanguageOptions" | "finalize", WeakSet<WeakKey>>` | const | `new Map(
  forbiddenMethods.map(methodName => [methodName, new WeakSet()]),
)` | ✗ |
| `original` | `Prototype[MethodName]` | const | `prototype[methodName]` | ✗ |
| `called` | `WeakSet<WeakKey>` | const | `forbiddenMethodCalls.get(methodName)!` | ✗ |
| `constructor` | `typeof RuleTester` | const | `this.constructor as typeof RuleTester` | ✗ |
| `basePath` | `string | undefined` | let/var | `this.#testerConfig.languageOptions.parserOptions?.tsconfigRootDir` | ✗ |
| `linter` | `any` | const | `new Linter({
          configType: 'flat',
          cwd: basePath,
        })` | ✗ |
| `resolvedOptions` | `ParserOptions` | const | `deepMerge(
        this.#testerConfig.languageOptions.parserOptions,
        testOptions,
      ) as ParserOptions` | ✗ |
| `filename` | `string` | const | `originalFilename ??
        (resolvedOptions.ecmaFeatures?.jsx
          ? this.#testerConfig.defaultFilenames.tsx
          : this.#testerConfig.defaultFilenames.ts)` | ✗ |
| `normalizedTests` | `{ invalid: InvalidTestCase<MessageIds, Options>[]; valid: ValidTestCase<Options>[]; }` | const | `{
      invalid: rawTests.invalid.map(normalizeTest),
      valid: rawTests.valid
        .map(test => {
          if (typeof test === 'string') {
            return { code: test };
          }
          return test;
        })
        .map(normalizeTest),
    }` | ✗ |
| `allTestsIterator` | `{ [Symbol.iterator](): Generator<ValidTestCase<Options>, void, any>; }` | const | `{
      *[Symbol.iterator](): Generator<ValidTestCase<Options>, void> {
        for (const testCase of normalizedTests.valid) {
          yield testCase;
        }
        for (const testCase of normalizedTests.invalid) {
          yield testCase;
        }
      },
    }` | ✗ |
| `constructor` | `typeof RuleTester` | const | `this.constructor as typeof RuleTester` | ✗ |
| `scenarioErrors` | `string[]` | const | `[]` | ✗ |
| `seenValidTestCases` | `Set<string>` | const | `new Set<string>()` | ✗ |
| `seenInvalidTestCases` | `Set<string>` | const | `new Set<string>()` | ✗ |
| `code` | `any` | let/var | `*not shown*` | ✗ |
| `filename` | `any` | let/var | `*not shown*` | ✗ |
| `beforeAST` | `TSESTree.Program` | let/var | `*not shown*` | ✗ |
| `afterAST` | `TSESTree.Program` | let/var | `*not shown*` | ✗ |
| `itemConfig` | `Record<string, unknown>` | const | `{ ...item }` | ✗ |
| `prefixedRuleName` | `string` | const | ``${RULE_TESTER_PLUGIN_PREFIX}${ruleName}`` | ✗ |
| `field` | `any` | const | `error.dataPath[0] === '.'
                ? error.dataPath.slice(1)
                : error.dataPath` | ✗ |
| `initialMessages` | `Linter.LintMessage[] | null` | let/var | `null` | ✗ |
| `messages` | `Linter.LintMessage[] | null` | let/var | `null` | ✗ |
| `fixedResult` | `SourceCodeFixer.AppliedFixes | null` | let/var | `null` | ✗ |
| `passNumber` | `number` | let/var | `0` | ✗ |
| `outputs` | `string[]` | const | `[]` | ✗ |
| `SourceCodePrototype` | `Record<"applyInlineConfig" | "applyLanguageOptions" | "finalize", ForbiddenFunction>` | const | `SourceCode.prototype as Record<
        ForbiddenMethodName,
        ForbiddenFunction
      >` | ✗ |
| `item` | `ValidTestCase<Options>` | const | `typeof itemIn === 'object' ? itemIn : { code: itemIn }` | ✗ |
| `messages` | `Linter.LintMessage[]` | const | `result.messages` | ✗ |
| `ruleHasMetaMessages` | `boolean` | const | `hasOwnProperty(rule, 'meta') && hasOwnProperty(rule.meta, 'messages')` | ✗ |
| `friendlyIDList` | `string` | const | `ruleHasMetaMessages
      ? `[${Object.keys(rule.meta.messages)
          .map(key => `'${key}'`)
          .join(', ')}]`
      : null` | ✗ |
| `seenMessageIndices` | `Map<string, number>` | const | `new Map<string, number>()` | ✗ |
| `suggestionMessage` | `any` | const | `message.suggestions[i].desc` | ✗ |
| `error` | `TestCaseError<MessageIds>` | const | `item.errors[i]` | ✗ |
| `message` | `any` | const | `messages[i]` | ✗ |
| `unformattedOriginalMessage` | `any` | const | `rule.meta.messages[error.messageId]` | ✗ |
| `expectsSuggestions` | `boolean` | const | `Array.isArray(error.suggestions)
              ? error.suggestions.length > 0
              : Boolean(error.suggestions)` | ✗ |
| `hasSuggestions` | `boolean` | const | `message.suggestions != null` | ✗ |
| `messageSuggestions` | `any` | const | `message.suggestions!` | ✗ |
| `actualSuggestion` | `any` | const | `messageSuggestions[index]` | ✗ |
| `suggestionPrefix` | `string` | const | ``Error Suggestion at index ${index}:`` | ✗ |
| `expectedDesc` | `string` | const | `expectedSuggestion.desc as string` | ✗ |
| `unformattedMetaMessage` | `any` | const | `rule.meta.messages[expectedSuggestion.messageId]` | ✗ |
| `codeWithAppliedSuggestion` | `string` | const | `SourceCodeFixer.applyFixes(item.code, [
                        actualSuggestion,
                      ]).output` | ✗ |


---

## Functions

### `throwForbiddenMethodError(methodName: MethodName, prototype: Prototype): Prototype[MethodName]`

<details><summary>Code</summary>

```ts
function throwForbiddenMethodError<
  MethodName extends ForbiddenMethodName,
  Prototype extends Record<MethodName, ForbiddenFunction>,
>(methodName: MethodName, prototype: Prototype): Prototype[MethodName] {
  const original = prototype[methodName];

  return function (this: WeakKey, ...args: Parameters<Prototype[MethodName]>) {
    // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
    const called = forbiddenMethodCalls.get(methodName)!;

    if (!called.has(this)) {
      called.add(this);

      return original.apply(this, args);
    }

    throw new Error(
      `\`SourceCode#${methodName}()\` cannot be called inside a rule.`,
    );
  } as Prototype[MethodName];
}
```
</details>

- **JSDoc**:
```ts
/**
 * Function to replace forbidden `SourceCode` methods. Allows just one call per method.
 * @param methodName The name of the method to forbid.
 * @param prototype The prototype with the original method to call.
 * @returns The function that throws the error.
 */
```

- **Parameters**:
  - `methodName: MethodName`
  - `prototype: Prototype`
- **Return Type**: `Prototype[MethodName]`
- **Calls**:
  - `forbiddenMethodCalls.get`
  - `called.has`
  - `called.add`
  - `original.apply`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
```

### `getMessagePlaceholders(message: string): string[]`

<details><summary>Code</summary>

```ts
function getMessagePlaceholders(message: string): string[] {
  const matcher = getPlaceholderMatcher();

  return Array.from(message.matchAll(matcher), ([, name]) => name.trim());
}
```
</details>

- **JSDoc**:
```ts
/**
 * Extracts names of {{ placeholders }} from the reported message.
 * @param message Reported message
 * @returns Array of placeholder names
 */
```

- **Parameters**:
  - `message: string`
- **Return Type**: `string[]`
- **Calls**:
  - `getPlaceholderMatcher (from ./utils/interpolate)`
  - `Array.from`
  - `message.matchAll`
  - `name.trim`
### `getUnsubstitutedMessagePlaceholders(message: string, raw: string, data: Record<string, unknown>): string[]`

<details><summary>Code</summary>

```ts
function getUnsubstitutedMessagePlaceholders(
  message: string,
  raw: string,
  data: Record<string, unknown> = {},
): string[] {
  const unsubstituted = getMessagePlaceholders(message);

  if (unsubstituted.length === 0) {
    return [];
  }

  // Remove false positives by only counting placeholders in the raw message, which were not provided in the data matcher or added with a data property
  const known = getMessagePlaceholders(raw);
  const provided = Object.keys(data);

  return unsubstituted.filter(
    name => known.includes(name) && !provided.includes(name),
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns the placeholders in the reported messages but
 * only includes the placeholders available in the raw message and not in the provided data.
 * @param message The reported message
 * @param raw The raw message specified in the rule meta.messages
 * @param data The passed
 * @returns Missing placeholder names
 */
```

- **Parameters**:
  - `message: string`
  - `raw: string`
  - `data: Record<string, unknown>`
- **Return Type**: `string[]`
- **Calls**:
  - `getMessagePlaceholders`
  - `Object.keys`
  - `unsubstituted.filter`
  - `known.includes`
  - `provided.includes`
- **Internal Comments**:
```
// Remove false positives by only counting placeholders in the raw message, which were not provided in the data matcher or added with a data property (x2)
```

### `RuleTester.#getLinterForFilename(filename: string | undefined): Linter`

<details><summary>Code</summary>

```ts
#getLinterForFilename(filename: string | undefined): Linter {
    let basePath: string | undefined =
      this.#testerConfig.languageOptions.parserOptions?.tsconfigRootDir;
    // For an absolute path (`/foo.ts`), or a path that steps
    // up (`../foo.ts`), resolve the path relative to the base
    // path (using the current working directory if the parser
    // options did not specify a base path) and use the file's
    // root as the base path so that the file is under the base
    // path. For any other path, which would just be a plain
    // file name (`foo.ts`), don't change the base path.
    if (
      filename != null &&
      (path.isAbsolute(filename) || filename.startsWith('..'))
    ) {
      basePath = path.parse(
        path.resolve(basePath ?? process.cwd(), filename),
      ).root;
    }

    let linterForBasePath = this.#lintersByBasePath.get(basePath);
    if (!linterForBasePath) {
      linterForBasePath = (() => {
        const linter = new Linter({
          configType: 'flat',
          cwd: basePath,
        });

        // This nonsense is a workaround for https://github.com/jestjs/jest/issues/14840
        // see also https://github.com/typescript-eslint/typescript-eslint/issues/8942
        //
        // For some reason rethrowing exceptions skirts around the circular JSON error.
        const oldVerify = linter.verify.bind(linter);
        linter.verify = (
          ...args: Parameters<Linter['verify']>
        ): ReturnType<Linter['verify']> => {
          try {
            return oldVerify(...args);
          } catch (error) {
            throw new Error('Caught an error while linting', {
              cause: error,
            });
          }
        };

        return linter;
      })();
      this.#lintersByBasePath.set(basePath, linterForBasePath);
    }
    return linterForBasePath;
  }
```
</details>

- **Parameters**:
  - `filename: string | undefined`
- **Return Type**: `Linter`
- **Calls**:
  - `path.isAbsolute`
  - `filename.startsWith`
  - `path.parse`
  - `path.resolve`
  - `process.cwd`
  - `this.#lintersByBasePath.get`
  - `complex_call_7856`
  - `linter.verify.bind`
  - `oldVerify`
  - `this.#lintersByBasePath.set`
- **Internal Comments**:
```
// For an absolute path (`/foo.ts`), or a path that steps
// up (`../foo.ts`), resolve the path relative to the base
// path (using the current working directory if the parser
// options did not specify a base path) and use the file's
// root as the base path so that the file is under the base
// path. For any other path, which would just be a plain
// file name (`foo.ts`), don't change the base path.
// This nonsense is a workaround for https://github.com/jestjs/jest/issues/14840 (x2)
// see also https://github.com/typescript-eslint/typescript-eslint/issues/8942 (x2)
// (x2)
// For some reason rethrowing exceptions skirts around the circular JSON error. (x2)
```

### `RuleTester.setDefaultConfig(config: RuleTesterConfig): void`

<details><summary>Code</summary>

```ts
static setDefaultConfig(config: RuleTesterConfig): void {
    if (typeof config !== 'object' || config == null) {
      throw new TypeError(
        'RuleTester.setDefaultConfig: config must be an object',
      );
    }
    // Make sure the rules object exists since it is assumed to exist later
    defaultConfig = deepMerge(
      defaultConfig,
      // @ts-expect-error -- no index signature
      config,
    ) as TesterConfigWithDefaults;
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Set the configuration to use for all future tests
   */
```

- **Parameters**:
  - `config: RuleTesterConfig`
- **Return Type**: `void`
- **Calls**:
  - `deepMerge (from @typescript-eslint/utils/eslint-utils)`
- **Internal Comments**:
```
// Make sure the rules object exists since it is assumed to exist later (x3)
// @ts-expect-error -- no index signature
```

### `RuleTester.getDefaultConfig(): Readonly<RuleTesterConfig>`

<details><summary>Code</summary>

```ts
static getDefaultConfig(): Readonly<RuleTesterConfig> {
    return defaultConfig;
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Get the current configuration used for all tests
   */
```

- **Return Type**: `Readonly<RuleTesterConfig>`
### `RuleTester.resetDefaultConfig(): void`

<details><summary>Code</summary>

```ts
static resetDefaultConfig(): void {
    defaultConfig = merge({}, testerDefaultConfig);
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Reset the configuration to the initial configuration of the tester removing
   * any changes made until now.
   */
```

- **Return Type**: `void`
- **Calls**:
  - `merge (from lodash.merge)`
### `RuleTester.only(item: string | ValidTestCase<Options>): ValidTestCase<Options>`

<details><summary>Code</summary>

```ts
static only<Options extends readonly unknown[]>(
    item: string | ValidTestCase<Options>,
  ): ValidTestCase<Options>;
```
</details>

- **JSDoc**:
```ts
/**
   * Adds the `only` property to a test to run it in isolation.
   */
```

- **Parameters**:
  - `item: string | ValidTestCase<Options>`
- **Return Type**: `ValidTestCase<Options>`
### `RuleTester.only(item: InvalidTestCase<MessageIds, Options>): InvalidTestCase<MessageIds, Options>`

<details><summary>Code</summary>

```ts
static only<MessageIds extends string, Options extends readonly unknown[]>(
    item: InvalidTestCase<MessageIds, Options>,
  ): InvalidTestCase<MessageIds, Options>;
```
</details>

- **JSDoc**:
```ts
/**
   * Adds the `only` property to a test to run it in isolation.
   */
```

- **Parameters**:
  - `item: InvalidTestCase<MessageIds, Options>`
- **Return Type**: `InvalidTestCase<MessageIds, Options>`
### `RuleTester.only(item: | string
      | InvalidTestCase<MessageIds, Options>
      | ValidTestCase<Options>): InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>`

<details><summary>Code</summary>

```ts
static only<MessageIds extends string, Options extends readonly unknown[]>(
    item:
      | string
      | InvalidTestCase<MessageIds, Options>
      | ValidTestCase<Options>,
  ): InvalidTestCase<MessageIds, Options> | ValidTestCase<Options> {
    if (typeof item === 'string') {
      return { code: item, only: true };
    }

    return { ...item, only: true };
  }
```
</details>

- **Parameters**:
  - `item: | string
      | InvalidTestCase<MessageIds, Options>
      | ValidTestCase<Options>`
- **Return Type**: `InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>`
### `RuleTester.#normalizeTests(rawTests: RunTests<MessageIds, Options>): NormalizedRunTests<MessageIds, Options>`

<details><summary>Code</summary>

```ts
#normalizeTests<
    MessageIds extends string,
    Options extends readonly unknown[],
  >(
    rawTests: RunTests<MessageIds, Options>,
  ): NormalizedRunTests<MessageIds, Options> {
    /*
    Automatically add a filename to the tests to enable type-aware tests to "just work".
    This saves users having to verbosely and manually add the filename to every
    single test case.
    Hugely helps with the string-based valid test cases as it means they don't
    need to be made objects!
    */
    const getFilename = (
      originalFilename: string | undefined,
      testOptions: ParserOptions | undefined,
    ): string => {
      const resolvedOptions = deepMerge(
        this.#testerConfig.languageOptions.parserOptions,
        testOptions,
      ) as ParserOptions;
      const filename =
        originalFilename ??
        (resolvedOptions.ecmaFeatures?.jsx
          ? this.#testerConfig.defaultFilenames.tsx
          : this.#testerConfig.defaultFilenames.ts);
      if (resolvedOptions.project) {
        return path.join(
          resolvedOptions.tsconfigRootDir ?? process.cwd(),
          filename,
        );
      }
      return filename;
    };
    const normalizeTest = <
      MessageIds extends string,
      Options extends readonly unknown[],
      T extends InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
    >(
      test: T,
    ): T => {
      const { languageOptions = {} } = test;
      if (languageOptions.parser === parser) {
        throw new Error(DUPLICATE_PARSER_ERROR_MESSAGE);
      }
      return {
        ...test,
        filename: getFilename(test.filename, languageOptions.parserOptions),
        languageOptions: {
          ...languageOptions,
          parserOptions: {
            // Re-running simulates --fix mode, which implies an isolated program
            // (i.e. parseAndGenerateServicesCalls[test.filename] > 1).
            disallowAutomaticSingleRunInference: true,
            ...languageOptions.parserOptions,
          },
        },
      };
    };

    const normalizedTests = {
      invalid: rawTests.invalid.map(normalizeTest),
      valid: rawTests.valid
        .map(test => {
          if (typeof test === 'string') {
            return { code: test };
          }
          return test;
        })
        .map(normalizeTest),
    };

    // convenience iterator to make it easy to loop all tests without a concat
    const allTestsIterator = {
      *[Symbol.iterator](): Generator<ValidTestCase<Options>, void> {
        for (const testCase of normalizedTests.valid) {
          yield testCase;
        }
        for (const testCase of normalizedTests.invalid) {
          yield testCase;
        }
      },
    };

    const hasOnly = ((): boolean => {
      for (const test of allTestsIterator) {
        if (test.only) {
          return true;
        }
      }
      return false;
    })();
    if (hasOnly) {
      // if there is an `only: true` - don't try apply constraints - assume that
      // we are in "local development" mode rather than "CI validation" mode
      return normalizedTests;
    }

    const hasConstraints = ((): boolean => {
      for (const test of allTestsIterator) {
        if (
          test.dependencyConstraints &&
          Object.keys(test.dependencyConstraints).length > 0
        ) {
          return true;
        }
      }
      return false;
    })();
    if (!hasConstraints) {
      return normalizedTests;
    }

    /*
    Mark all unsatisfactory tests as `skip: true`.
    We do this instead of just omitting the tests entirely because it gives the
    test framework the opportunity to log the test as skipped rather than the test
    just disappearing without a trace.
    */
    const maybeMarkAsOnly = <
      T extends InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
    >(
      test: T,
    ): T => {
      return {
        ...test,
        skip: !satisfiesAllDependencyConstraints(test.dependencyConstraints),
      };
    };
    normalizedTests.valid = normalizedTests.valid.map(maybeMarkAsOnly);
    normalizedTests.invalid = normalizedTests.invalid.map(maybeMarkAsOnly);

    return normalizedTests;
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Define a rule for one particular run of tests.
   */
```

- **Parameters**:
  - `rawTests: RunTests<MessageIds, Options>`
- **Return Type**: `NormalizedRunTests<MessageIds, Options>`
- **Calls**:
  - `deepMerge (from @typescript-eslint/utils/eslint-utils)`
  - `path.join`
  - `process.cwd`
  - `getFilename`
  - `rawTests.invalid.map`
  - `rawTests.valid
        .map(test => {
          if (typeof test === 'string') {
            return { code: test };
          }
          return test;
        })
        .map`
  - `complex_call_13281`
  - `complex_call_13681`
  - `Object.keys`
  - `satisfiesAllDependencyConstraints (from ./utils/dependencyConstraints)`
  - `normalizedTests.valid.map`
  - `normalizedTests.invalid.map`
- **Internal Comments**:
```
/*
    Automatically add a filename to the tests to enable type-aware tests to "just work".
    This saves users having to verbosely and manually add the filename to every
    single test case.
    Hugely helps with the string-based valid test cases as it means they don't
    need to be made objects!
    */ (x2)
// Re-running simulates --fix mode, which implies an isolated program (x2)
// (i.e. parseAndGenerateServicesCalls[test.filename] > 1). (x2)
// convenience iterator to make it easy to loop all tests without a concat (x2)
// if there is an `only: true` - don't try apply constraints - assume that
// we are in "local development" mode rather than "CI validation" mode
/*
    Mark all unsatisfactory tests as `skip: true`.
    We do this instead of just omitting the tests entirely because it gives the
    test framework the opportunity to log the test as skipped rather than the test
    just disappearing without a trace.
    */ (x2)
```

### `RuleTester.defineRule(name: string, rule: AnyRuleModule): void`

<details><summary>Code</summary>

```ts
defineRule(name: string, rule: AnyRuleModule): void {
    this.#rules[name] = {
      ...rule,
      // Create a wrapper rule that freezes the `context` properties.
      create(context): RuleListener {
        freezeDeeply(context.options);
        freezeDeeply(context.settings);
        freezeDeeply(context.parserOptions);

        return (typeof rule === 'function' ? rule : rule.create)(context);
      },
    };
  }
```
</details>

- **Parameters**:
  - `name: string`
  - `rule: AnyRuleModule`
- **Return Type**: `void`
- **Calls**:
  - `freezeDeeply (from ./utils/freezeDeeply)`
  - `complex_call_15070`
- **Internal Comments**:
```
// Create a wrapper rule that freezes the `context` properties. (x2)
```

### `RuleTester.#runHook(item: InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>, prop: keyof Pick<typeof item, 'after' | 'before'>): void`

<details><summary>Code</summary>

```ts
#runHook<MessageIds extends string, Options extends readonly unknown[]>(
    item: InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
    prop: keyof Pick<typeof item, 'after' | 'before'>,
  ): void {
    if (hasOwnProperty(item, prop)) {
      assert.strictEqual(
        typeof item[prop],
        'function',
        `Optional test case property '${prop}' must be a function`,
      );
      item[prop]();
    }
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Runs a hook on the given item when it's assigned to the given property
   * @throws {Error} If the property is not a function or that function throws an error
   */
```

- **Parameters**:
  - `item: InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>`
  - `prop: keyof Pick<typeof item, 'after' | 'before'>`
- **Return Type**: `void`
- **Calls**:
  - `hasOwnProperty (from ./utils/hasOwnProperty)`
  - `assert.strictEqual`
  - `complex_call_15736`
### `RuleTester.run(ruleName: string, rule: RuleModule<MessageIds, Options>, test: RunTests<TSUtils.NoInfer<MessageIds>, TSUtils.NoInfer<Options>>): void`

<details><summary>Code</summary>

```ts
run<MessageIds extends string, Options extends readonly unknown[]>(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    test: RunTests<TSUtils.NoInfer<MessageIds>, TSUtils.NoInfer<Options>>,
  ): void {
    const constructor = this.constructor as typeof RuleTester;

    if (
      this.#testerConfig.dependencyConstraints &&
      !satisfiesAllDependencyConstraints(
        this.#testerConfig.dependencyConstraints,
      )
    ) {
      // for frameworks like mocha or jest that have a "skip" version of their function
      // we can provide a nice skipped test!
      constructor.describeSkip(ruleName, () => {
        constructor.it(
          'All tests skipped due to unsatisfied constructor dependency constraints',
          () => {
            // some frameworks error if there are no assertions
            assert.equal(true, true);
          },
        );
      });

      // don't run any tests because we don't match the base constraint
      return;
    }

    if (!test || typeof test !== 'object') {
      throw new TypeError(
        `Test Scenarios for rule ${ruleName} : Could not find test scenario object`,
      );
    }

    const scenarioErrors: string[] = [];
    REQUIRED_SCENARIOS.forEach(scenarioType => {
      if (!test[scenarioType]) {
        scenarioErrors.push(
          `Could not find any ${scenarioType} test scenarios`,
        );
      }
    });

    if (scenarioErrors.length > 0) {
      throw new Error(
        [
          `Test Scenarios for rule ${ruleName} is invalid:`,
          ...scenarioErrors,
        ].join('\n'),
      );
    }

    const seenValidTestCases = new Set<string>();
    const seenInvalidTestCases = new Set<string>();
    const normalizedTests = this.#normalizeTests(test);

    function getTestMethod(
      test: ValidTestCase<TSUtils.NoInfer<Options>>,
    ): 'it' | 'itOnly' | 'itSkip' {
      if (test.skip) {
        return 'itSkip';
      }
      if (test.only) {
        return 'itOnly';
      }
      return 'it';
    }

    /*
     * This creates a test suite and pipes all supplied info through
     * one of the templates above.
     */
    constructor.describe(ruleName, () => {
      if (normalizedTests.valid.length) {
        constructor.describe('valid', () => {
          normalizedTests.valid.forEach(valid => {
            const testName = ((): string => {
              if (valid.name == null || valid.name.length === 0) {
                return valid.code;
              }
              return valid.name;
            })();
            constructor[getTestMethod(valid)](sanitize(testName), () => {
              try {
                this.#runHook(valid, 'before');
                this.#testValidTemplate(
                  ruleName,
                  rule,
                  valid,
                  seenValidTestCases,
                );
              } finally {
                this.#runHook(valid, 'after');
              }
            });
          });
        });
      }

      if (normalizedTests.invalid.length) {
        constructor.describe('invalid', () => {
          normalizedTests.invalid.forEach(invalid => {
            const name = ((): string => {
              if (invalid.name == null || invalid.name.length === 0) {
                return invalid.code;
              }
              return invalid.name;
            })();
            constructor[getTestMethod(invalid)](sanitize(name), () => {
              try {
                this.#runHook(invalid, 'before');
                this.#testInvalidTemplate(
                  ruleName,
                  rule,
                  // no need to pass no infer type parameter down to private methods
                  invalid as InvalidTestCase<MessageIds, Options>,
                  seenInvalidTestCases,
                );
              } finally {
                this.#runHook(invalid, 'after');
              }
            });
          });
        });
      }
    });
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Adds a new rule test to execute.
   */
```

- **Parameters**:
  - `ruleName: string`
  - `rule: RuleModule<MessageIds, Options>`
  - `test: RunTests<TSUtils.NoInfer<MessageIds>, TSUtils.NoInfer<Options>>`
- **Return Type**: `void`
- **Calls**:
  - `satisfiesAllDependencyConstraints (from ./utils/dependencyConstraints)`
  - `constructor.describeSkip`
  - `constructor.it`
  - `assert.equal`
  - `REQUIRED_SCENARIOS.forEach`
  - `scenarioErrors.push`
  - `[
          `Test Scenarios for rule ${ruleName} is invalid:`,
          ...scenarioErrors,
        ].join`
  - `this.#normalizeTests`
  - `constructor.describe`
  - `normalizedTests.valid.forEach`
  - `complex_call_18161`
  - `complex_call_18359`
  - `getTestMethod`
  - `sanitize (from ./utils/validationHelpers)`
  - `this.#runHook`
  - `this.#testValidTemplate`
  - `normalizedTests.invalid.forEach`
  - `complex_call_18976`
  - `complex_call_19182`
  - `this.#testInvalidTemplate`
- **Internal Comments**:
```
// for frameworks like mocha or jest that have a "skip" version of their function (x4)
// we can provide a nice skipped test! (x4)
// some frameworks error if there are no assertions (x4)
// don't run any tests because we don't match the base constraint
/*
     * This creates a test suite and pipes all supplied info through
     * one of the templates above.
     */ (x4)
// no need to pass no infer type parameter down to private methods (x2)
```

### `RuleTester.runRuleForItem(ruleName: string, rule: RuleModule<MessageIds, Options>, item: InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>): {
    afterAST: TSESTree.Program;
    beforeAST: TSESTree.Program;
    config: RuleTesterConfig;
    filename?: string;
    messages: Linter.LintMessage[];
    outputs: string[];
  }`

<details><summary>Code</summary>

```ts
private runRuleForItem<
    MessageIds extends string,
    Options extends readonly unknown[],
  >(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    item: InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
  ): {
    afterAST: TSESTree.Program;
    beforeAST: TSESTree.Program;
    config: RuleTesterConfig;
    filename?: string;
    messages: Linter.LintMessage[];
    outputs: string[];
  } {
    this.defineRule(ruleName, rule);

    let config: TesterConfigWithDefaults = merge({}, this.#testerConfig, {
      files: ['**'],
      plugins: {
        [RULE_TESTER_PLUGIN]: {
          rules: {
            /**
             * Setup AST getters.
             * The goal is to check whether or not AST was modified when
             * running the rule under test.
             */
            'validate-ast': {
              create(): RuleListener {
                return {
                  Program(node: TSESTree.Program): void {
                    beforeAST = cloneDeeplyExcludesParent(node);
                  },
                  'Program:exit'(node: TSESTree.Program): void {
                    afterAST = node;
                  },
                };
              },
            },
            ...this.#rules,
          },
        },
      },
    });

    // Unlike other properties, we don't want to spread props between different parsers.
    config.languageOptions.parser =
      item.languageOptions?.parser ?? this.#testerConfig.languageOptions.parser;

    let code;
    let filename;
    let beforeAST: TSESTree.Program;
    let afterAST: TSESTree.Program;

    if (typeof item === 'string') {
      code = item;
    } else {
      code = item.code;

      /*
       * Assumes everything on the item is a config except for the
       * parameters used by this tester
       */
      const itemConfig: Record<string, unknown> = { ...item };

      for (const parameter of RULE_TESTER_PARAMETERS) {
        // eslint-disable-next-line @typescript-eslint/no-dynamic-delete
        delete itemConfig[parameter];
      }

      /*
       * Create the config object from the tester config and this item
       * specific configurations.
       */
      config = merge(config, itemConfig);
    }

    if (hasOwnProperty(item, 'only')) {
      assert.ok(
        typeof item.only === 'boolean',
        "Optional test case property 'only' must be a boolean",
      );
    }
    if (hasOwnProperty(item, 'filename')) {
      assert.ok(
        typeof item.filename === 'string',
        "Optional test case property 'filename' must be a string",
      );
      filename = item.filename;
    }

    const prefixedRuleName = `${RULE_TESTER_PLUGIN_PREFIX}${ruleName}`;

    if (hasOwnProperty(item, 'options')) {
      assert(Array.isArray(item.options), 'options must be an array');
      config.rules[prefixedRuleName] = ['error', ...item.options];
    } else {
      config.rules[prefixedRuleName] = 'error';
    }

    config.languageOptions ??= {};
    config.languageOptions.parser ??= defaultParser;
    config.languageOptions.parser = wrapParser(config.languageOptions.parser);

    const schema = getRuleOptionsSchema(rule);

    if (schema) {
      ajv.validateSchema(schema);

      if (ajv.errors) {
        const errors = ajv.errors
          .map(error => {
            const field =
              error.dataPath[0] === '.'
                ? error.dataPath.slice(1)
                : error.dataPath;

            return `\t${field}: ${error.message}`;
          })
          .join('\n');

        throw new Error(
          [`Schema for rule ${ruleName} is invalid:`, errors].join(
            // no space after comma to match eslint core
            ',',
          ),
        );
      }

      /*
       * `ajv.validateSchema` checks for errors in the structure of the schema (by comparing the schema against a "meta-schema"),
       * and it reports those errors individually. However, there are other types of schema errors that only occur when compiling
       * the schema (e.g. using invalid defaults in a schema), and only one of these errors can be reported at a time. As a result,
       * the schema is compiled here separately from checking for `validateSchema` errors.
       */
      try {
        ajv.compile(schema);
      } catch (err) {
        throw new Error(
          `Schema for rule ${ruleName} is invalid: ${(err as Error).message}`,
        );
      }
    }

    validate(config, RULE_TESTER_PLUGIN, id => (id === ruleName ? rule : null));

    // Verify the code.
    let initialMessages: Linter.LintMessage[] | null = null;
    let messages: Linter.LintMessage[] | null = null;
    let fixedResult: SourceCodeFixer.AppliedFixes | null = null;
    let passNumber = 0;
    const outputs: string[] = [];
    const configWithoutCustomKeys = omitCustomConfigProperties(config);
    const linter = this.#getLinterForFilename(filename);

    do {
      passNumber++;

      const SourceCodePrototype = SourceCode.prototype as Record<
        ForbiddenMethodName,
        ForbiddenFunction
      >;

      const { applyInlineConfig, applyLanguageOptions, finalize } =
        SourceCodePrototype;

      try {
        forbiddenMethods.forEach(methodName => {
          SourceCodePrototype[methodName] = throwForbiddenMethodError(
            methodName,
            SourceCodePrototype,
          );
        });

        const actualConfig = merge(configWithoutCustomKeys, {
          languageOptions: {
            ...configWithoutCustomKeys.languageOptions,
            parserOptions: {
              ecmaVersion: 'latest',
              sourceType: 'module',
              ...configWithoutCustomKeys.languageOptions?.parserOptions,
            },
          },
          linterOptions: {
            reportUnusedDisableDirectives: 1,
            ...configWithoutCustomKeys.linterOptions,
          },
        });
        messages = linter.verify(code, actualConfig, filename);
      } finally {
        SourceCodePrototype.applyInlineConfig = applyInlineConfig;
        SourceCodePrototype.applyLanguageOptions = applyLanguageOptions;
        SourceCodePrototype.finalize = finalize;
      }

      initialMessages ??= messages;

      if (messages.length === 0) {
        break;
      }

      const fatalErrorMessage = messages.find(m => m.fatal);
      assert(
        !fatalErrorMessage,
        `A fatal parsing error occurred: ${fatalErrorMessage?.message}`,
      );

      fixedResult = SourceCodeFixer.applyFixes(code, messages);
      if (fixedResult.output === code) {
        break;
      }
      code = fixedResult.output;
      outputs.push(code);

      // Verify if autofix makes a syntax error or not.
      const errorMessageInFix = linter
        .verify(fixedResult.output, configWithoutCustomKeys, filename)
        .find(m => m.fatal);

      assert(
        !errorMessageInFix,
        [
          'A fatal parsing error occurred in autofix.',
          `Error: ${errorMessageInFix?.message}`,
          'Autofix output:',
          fixedResult.output,
        ].join('\n'),
      );
    } while (fixedResult.fixed && passNumber < 10);

    return {
      config,
      filename,
      messages: initialMessages,
      outputs,
      // is definitely assigned within the `@rule-tester/validate-ast` rule
      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      beforeAST: beforeAST!,
      // is definitely assigned within the `@rule-tester/validate-ast` rule
      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      afterAST: cloneDeeplyExcludesParent(afterAST!),
    };
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Run the rule for the given item
   * @throws {Error} If an invalid schema.
   * Use @private instead of #private to expose it for testing purposes
   */
```

- **Parameters**:
  - `ruleName: string`
  - `rule: RuleModule<MessageIds, Options>`
  - `item: InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>`
- **Return Type**: `{
    afterAST: TSESTree.Program;
    beforeAST: TSESTree.Program;
    config: RuleTesterConfig;
    filename?: string;
    messages: Linter.LintMessage[];
    outputs: string[];
  }`
- **Calls**:
  - `this.defineRule`
  - `merge (from lodash.merge)`
  - `cloneDeeplyExcludesParent (from ./utils/cloneDeeplyExcludesParent)`
  - `hasOwnProperty (from ./utils/hasOwnProperty)`
  - `assert.ok`
  - `assert (from node:assert)`
  - `Array.isArray`
  - `wrapParser (from ./utils/validationHelpers)`
  - `getRuleOptionsSchema (from ./utils/getRuleOptionsSchema)`
  - `ajv.validateSchema`
  - `ajv.errors
          .map(error => {
            const field =
              error.dataPath[0] === '.'
                ? error.dataPath.slice(1)
                : error.dataPath;

            return `\t${field}: ${error.message}`;
          })
          .join`
  - `[`Schema for rule ${ruleName} is invalid:`, errors].join`
  - `ajv.compile`
  - `validate (from ./utils/config-validator)`
  - `omitCustomConfigProperties (from ./utils/omitCustomConfigProperties)`
  - `this.#getLinterForFilename`
  - `forbiddenMethods.forEach`
  - `throwForbiddenMethodError`
  - `linter.verify`
  - `messages.find`
  - `SourceCodeFixer.applyFixes`
  - `outputs.push`
  - `linter
        .verify(fixedResult.output, configWithoutCustomKeys, filename)
        .find`
  - `[
          'A fatal parsing error occurred in autofix.',
          `Error: ${errorMessageInFix?.message}`,
          'Autofix output:',
          fixedResult.output,
        ].join`
- **Internal Comments**:
```
/**
             * Setup AST getters.
             * The goal is to check whether or not AST was modified when
             * running the rule under test.
             */ (x2)
// Unlike other properties, we don't want to spread props between different parsers. (x5)
/*
       * Assumes everything on the item is a config except for the
       * parameters used by this tester
       */ (x2)
// eslint-disable-next-line @typescript-eslint/no-dynamic-delete (x2)
/*
       * Create the config object from the tester config and this item
       * specific configurations.
       */ (x3)
// no space after comma to match eslint core
/*
       * `ajv.validateSchema` checks for errors in the structure of the schema (by comparing the schema against a "meta-schema"),
       * and it reports those errors individually. However, there are other types of schema errors that only occur when compiling
       * the schema (e.g. using invalid defaults in a schema), and only one of these errors can be reported at a time. As a result,
       * the schema is compiled here separately from checking for `validateSchema` errors.
       */
// Verify the code. (x2)
// Verify if autofix makes a syntax error or not. (x2)
// is definitely assigned within the `@rule-tester/validate-ast` rule (x4)
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x4)
```

### `RuleTester.#testValidTemplate(ruleName: string, rule: RuleModule<MessageIds, Options>, itemIn: string | ValidTestCase<Options>, seenValidTestCases: Set<string>): void`

<details><summary>Code</summary>

```ts
#testValidTemplate<
    MessageIds extends string,
    Options extends readonly unknown[],
  >(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    itemIn: string | ValidTestCase<Options>,
    seenValidTestCases: Set<string>,
  ): void {
    const item: ValidTestCase<Options> =
      typeof itemIn === 'object' ? itemIn : { code: itemIn };

    assert.ok(
      typeof item.code === 'string',
      "Test case must specify a string value for 'code'",
    );
    if (item.name) {
      assert.ok(
        typeof item.name === 'string',
        "Optional test case property 'name' must be a string",
      );
    }

    checkDuplicateTestCase(item, seenValidTestCases);

    const result = this.runRuleForItem(ruleName, rule, item);
    const messages = result.messages;

    assert.strictEqual(
      messages.length,
      0,
      util.format(
        'Should have no errors but had %d: %s',
        messages.length,
        util.inspect(messages),
      ),
    );

    assertASTDidntChange(result.beforeAST, result.afterAST);
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Check if the template is valid or not
   * all valid cases go through this
   */
```

- **Parameters**:
  - `ruleName: string`
  - `rule: RuleModule<MessageIds, Options>`
  - `itemIn: string | ValidTestCase<Options>`
  - `seenValidTestCases: Set<string>`
- **Return Type**: `void`
- **Calls**:
  - `assert.ok`
  - `checkDuplicateTestCase`
  - `this.runRuleForItem`
  - `assert.strictEqual`
  - `util.format`
  - `util.inspect`
  - `assertASTDidntChange`
### `RuleTester.#testInvalidTemplate(ruleName: string, rule: RuleModule<MessageIds, Options>, item: InvalidTestCase<MessageIds, Options>, seenInvalidTestCases: Set<string>): void`

<details><summary>Code</summary>

```ts
#testInvalidTemplate<
    MessageIds extends string,
    Options extends readonly unknown[],
  >(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    item: InvalidTestCase<MessageIds, Options>,
    seenInvalidTestCases: Set<string>,
  ): void {
    assert.ok(
      typeof item.code === 'string',
      "Test case must specify a string value for 'code'",
    );
    if (item.name) {
      assert.ok(
        typeof item.name === 'string',
        "Optional test case property 'name' must be a string",
      );
    }
    assert.ok(
      item.errors || item.errors === 0,
      `Did not specify errors for an invalid test of ${ruleName}`,
    );

    if (Array.isArray(item.errors) && item.errors.length === 0) {
      assert.fail('Invalid cases must have at least one error');
    }

    checkDuplicateTestCase(item, seenInvalidTestCases);

    const ruleHasMetaMessages =
      hasOwnProperty(rule, 'meta') && hasOwnProperty(rule.meta, 'messages');
    const friendlyIDList = ruleHasMetaMessages
      ? `[${Object.keys(rule.meta.messages)
          .map(key => `'${key}'`)
          .join(', ')}]`
      : null;

    const result = this.runRuleForItem(ruleName, rule, item);
    const messages = result.messages.map(message => ({
      ...message,
      ...(message.ruleId && {
        ruleId: message.ruleId.startsWith(RULE_TESTER_PLUGIN_PREFIX)
          ? message.ruleId.slice(RULE_TESTER_PLUGIN_PREFIX.length)
          : message.ruleId,
      }),
    }));

    for (const message of messages) {
      if (hasOwnProperty(message, 'suggestions')) {
        const seenMessageIndices = new Map<string, number>();

        for (let i = 0; i < message.suggestions.length; i += 1) {
          const suggestionMessage = message.suggestions[i].desc;
          const previous = seenMessageIndices.get(suggestionMessage);

          assert.ok(
            !seenMessageIndices.has(suggestionMessage),
            `Suggestion message '${suggestionMessage}' reported from suggestion ${i} was previously reported by suggestion ${previous}. Suggestion messages should be unique within an error.`,
          );
          seenMessageIndices.set(suggestionMessage, i);
        }
      }
    }

    if (typeof item.errors === 'number') {
      if (item.errors === 0) {
        assert.fail("Invalid cases must have 'error' value greater than 0");
      }

      assert.strictEqual(
        messages.length,
        item.errors,
        util.format(
          'Should have %d error%s but had %d: %s',
          item.errors,
          item.errors === 1 ? '' : 's',
          messages.length,
          util.inspect(messages),
        ),
      );
    } else {
      assert.strictEqual(
        messages.length,
        item.errors.length,
        util.format(
          'Should have %d error%s but had %d: %s',
          item.errors.length,
          item.errors.length === 1 ? '' : 's',
          messages.length,
          util.inspect(messages),
        ),
      );

      const hasMessageOfThisRule = messages.some(m => m.ruleId === ruleName);

      // console.log({ messages });
      for (let i = 0, l = item.errors.length; i < l; i++) {
        const error = item.errors[i];
        const message = messages[i];

        assert(
          hasMessageOfThisRule,
          'Error rule name should be the same as the name of the rule being tested',
        );

        if (typeof error === 'string' || error instanceof RegExp) {
          // Just an error message.
          assertMessageMatches(message.message, error);
          assert.ok(
            message.suggestions == null,
            `Error at index ${i} has suggestions. Please convert the test error into an object and specify 'suggestions' property on it to test suggestions.`,
          );
        } else if (typeof error === 'object' && error != null) {
          /*
           * Error object.
           * This may have a message, messageId, data, node type, line, and/or
           * column.
           */

          Object.keys(error).forEach(propertyName => {
            assert.ok(
              ERROR_OBJECT_PARAMETERS.has(propertyName),
              `Invalid error property name '${propertyName}'. Expected one of ${FRIENDLY_ERROR_OBJECT_PARAMETER_LIST}.`,
            );
          });

          // @ts-expect-error -- we purposely don't define `message` on our types as the current standard is `messageId`
          if (hasOwnProperty(error, 'message')) {
            assert.ok(
              !hasOwnProperty(error, 'messageId'),
              "Error should not specify both 'message' and a 'messageId'.",
            );
            assert.ok(
              !hasOwnProperty(error, 'data'),
              "Error should not specify both 'data' and 'message'.",
            );
            assertMessageMatches(
              message.message,
              // @ts-expect-error -- we purposely don't define `message` on our types as the current standard is `messageId`
              error.message as unknown,
            );
          } else if (hasOwnProperty(error, 'messageId')) {
            assert.ok(
              ruleHasMetaMessages,
              "Error can not use 'messageId' if rule under test doesn't define 'meta.messages'.",
            );
            if (!hasOwnProperty(rule.meta.messages, error.messageId)) {
              assert(
                false,
                `Invalid messageId '${error.messageId}'. Expected one of ${friendlyIDList}.`,
              );
            }
            assert.strictEqual(
              message.messageId,
              error.messageId,
              `messageId '${message.messageId}' does not match expected messageId '${error.messageId}'.`,
            );

            const unsubstitutedPlaceholders =
              getUnsubstitutedMessagePlaceholders(
                message.message,
                rule.meta.messages[message.messageId],
                error.data,
              );

            assert.ok(
              unsubstitutedPlaceholders.length === 0,
              `The reported message has ${unsubstitutedPlaceholders.length > 1 ? `unsubstituted placeholders: ${unsubstitutedPlaceholders.map(name => `'${name}'`).join(', ')}` : `an unsubstituted placeholder '${unsubstitutedPlaceholders[0]}'`}. Please provide the missing ${unsubstitutedPlaceholders.length > 1 ? 'values' : 'value'} via the 'data' property in the context.report() call.`,
            );

            if (hasOwnProperty(error, 'data')) {
              /*
               *  if data was provided, then directly compare the returned message to a synthetic
               *  interpolated message using the same message ID and data provided in the test.
               *  See https://github.com/eslint/eslint/issues/9890 for context.
               */
              const unformattedOriginalMessage =
                rule.meta.messages[error.messageId];
              const rehydratedMessage = interpolate(
                unformattedOriginalMessage,
                error.data,
              );

              assert.strictEqual(
                message.message,
                rehydratedMessage,
                `Hydrated message "${rehydratedMessage}" does not match "${message.message}"`,
              );
            }
          } else {
            assert.fail(
              "Test error must specify either a 'messageId' or 'message'.",
            );
          }

          if (error.type) {
            assert.strictEqual(
              message.nodeType,
              error.type,
              `Error type should be ${error.type}, found ${message.nodeType}`,
            );
          }

          if (hasOwnProperty(error, 'line')) {
            assert.strictEqual(
              message.line,
              error.line,
              `Error line should be ${error.line}`,
            );
          }

          if (hasOwnProperty(error, 'column')) {
            assert.strictEqual(
              message.column,
              error.column,
              `Error column should be ${error.column}`,
            );
          }

          if (hasOwnProperty(error, 'endLine')) {
            assert.strictEqual(
              message.endLine,
              error.endLine,
              `Error endLine should be ${error.endLine}`,
            );
          }

          if (hasOwnProperty(error, 'endColumn')) {
            assert.strictEqual(
              message.endColumn,
              error.endColumn,
              `Error endColumn should be ${error.endColumn}`,
            );
          }

          assert.ok(
            !message.suggestions || hasOwnProperty(error, 'suggestions'),
            `Error at index ${i} has suggestions. Please specify 'suggestions' property on the test error object.`,
          );
          if (hasOwnProperty(error, 'suggestions')) {
            // Support asserting there are no suggestions
            const expectsSuggestions = Array.isArray(error.suggestions)
              ? error.suggestions.length > 0
              : Boolean(error.suggestions);
            const hasSuggestions = message.suggestions != null;
            // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
            const messageSuggestions = message.suggestions!;

            if (!hasSuggestions && expectsSuggestions) {
              assert.ok(
                !error.suggestions,
                `Error should have suggestions on error with message: "${message.message}"`,
              );
            } else if (hasSuggestions) {
              assert.ok(
                expectsSuggestions,
                `Error should have no suggestions on error with message: "${message.message}"`,
              );
              if (typeof error.suggestions === 'number') {
                assert.strictEqual(
                  messageSuggestions.length,
                  error.suggestions,
                  // It is possible that error.suggestions is a number
                  // eslint-disable-next-line @typescript-eslint/restrict-template-expressions
                  `Error should have ${error.suggestions} suggestions. Instead found ${messageSuggestions.length} suggestions`,
                );
              } else if (Array.isArray(error.suggestions)) {
                assert.strictEqual(
                  messageSuggestions.length,
                  error.suggestions.length,
                  `Error should have ${error.suggestions.length} suggestions. Instead found ${messageSuggestions.length} suggestions`,
                );

                error.suggestions.forEach(
                  (expectedSuggestion: SuggestionOutput<MessageIds>, index) => {
                    assert.ok(
                      typeof expectedSuggestion === 'object' &&
                        expectedSuggestion != null,
                      "Test suggestion in 'suggestions' array must be an object.",
                    );
                    Object.keys(expectedSuggestion).forEach(propertyName => {
                      assert.ok(
                        SUGGESTION_OBJECT_PARAMETERS.has(propertyName),
                        `Invalid suggestion property name '${propertyName}'. Expected one of ${FRIENDLY_SUGGESTION_OBJECT_PARAMETER_LIST}.`,
                      );
                    });

                    const actualSuggestion = messageSuggestions[index];
                    const suggestionPrefix = `Error Suggestion at index ${index}:`;

                    // @ts-expect-error -- we purposely don't define `desc` on our types as the current standard is `messageId`
                    if (hasOwnProperty(expectedSuggestion, 'desc')) {
                      // @ts-expect-error -- we purposely don't define `desc` on our types as the current standard is `messageId`
                      const expectedDesc = expectedSuggestion.desc as string;

                      assert.ok(
                        !hasOwnProperty(expectedSuggestion, 'data'),
                        `${suggestionPrefix} Test should not specify both 'desc' and 'data'.`,
                      );
                      assert.ok(
                        !hasOwnProperty(expectedSuggestion, 'messageId'),
                        `${suggestionPrefix} Test should not specify both 'desc' and 'messageId'.`,
                      );
                      assert.strictEqual(
                        actualSuggestion.desc,
                        expectedDesc,
                        `${suggestionPrefix} desc should be "${expectedDesc}" but got "${actualSuggestion.desc}" instead.`,
                      );
                    } else if (
                      hasOwnProperty(expectedSuggestion, 'messageId')
                    ) {
                      assert.ok(
                        ruleHasMetaMessages,
                        `${suggestionPrefix} Test can not use 'messageId' if rule under test doesn't define 'meta.messages'.`,
                      );
                      assert.ok(
                        hasOwnProperty(
                          rule.meta.messages,
                          expectedSuggestion.messageId,
                        ),
                        `${suggestionPrefix} Test has invalid messageId '${expectedSuggestion.messageId}', the rule under test allows only one of ${friendlyIDList}.`,
                      );
                      assert.strictEqual(
                        actualSuggestion.messageId,
                        expectedSuggestion.messageId,
                        `${suggestionPrefix} messageId should be '${expectedSuggestion.messageId}' but got '${actualSuggestion.messageId}' instead.`,
                      );

                      const unsubstitutedPlaceholders =
                        getUnsubstitutedMessagePlaceholders(
                          actualSuggestion.desc,
                          rule.meta.messages[expectedSuggestion.messageId],
                          expectedSuggestion.data,
                        );

                      assert.ok(
                        unsubstitutedPlaceholders.length === 0,
                        `The message of the suggestion has ${unsubstitutedPlaceholders.length > 1 ? `unsubstituted placeholders: ${unsubstitutedPlaceholders.map(name => `'${name}'`).join(', ')}` : `an unsubstituted placeholder '${unsubstitutedPlaceholders[0]}'`}. Please provide the missing ${unsubstitutedPlaceholders.length > 1 ? 'values' : 'value'} via the 'data' property for the suggestion in the context.report() call.`,
                      );

                      if (hasOwnProperty(expectedSuggestion, 'data')) {
                        const unformattedMetaMessage =
                          rule.meta.messages[expectedSuggestion.messageId];
                        const rehydratedDesc = interpolate(
                          unformattedMetaMessage,
                          expectedSuggestion.data,
                        );

                        assert.strictEqual(
                          actualSuggestion.desc,
                          rehydratedDesc,
                          `${suggestionPrefix} Hydrated test desc "${rehydratedDesc}" does not match received desc "${actualSuggestion.desc}".`,
                        );
                      }
                    } else if (hasOwnProperty(expectedSuggestion, 'data')) {
                      assert.fail(
                        `${suggestionPrefix} Test must specify 'messageId' if 'data' is used.`,
                      );
                    } else {
                      assert.fail(
                        `${suggestionPrefix} Test must specify either 'messageId' or 'desc'.`,
                      );
                    }

                    assert.ok(
                      hasOwnProperty(expectedSuggestion, 'output'),
                      `${suggestionPrefix} The "output" property is required.`,
                    );
                    const codeWithAppliedSuggestion =
                      SourceCodeFixer.applyFixes(item.code, [
                        actualSuggestion,
                      ]).output;

                    // Verify if suggestion fix makes a syntax error or not.
                    const errorMessageInSuggestion = this.#getLinterForFilename(
                      item.filename,
                    )
                      .verify(
                        codeWithAppliedSuggestion,
                        omitCustomConfigProperties(result.config),
                        result.filename,
                      )
                      .find(m => m.fatal);

                    assert(
                      !errorMessageInSuggestion,
                      [
                        'A fatal parsing error occurred in suggestion fix.',
                        `Error: ${errorMessageInSuggestion?.message}`,
                        'Suggestion output:',
                        codeWithAppliedSuggestion,
                      ].join('\n'),
                    );

                    assert.strictEqual(
                      codeWithAppliedSuggestion,
                      expectedSuggestion.output,
                      `Expected the applied suggestion fix to match the test suggestion output for suggestion at index: ${index} on error with message: "${message.message}"`,
                    );
                    assert.notStrictEqual(
                      expectedSuggestion.output,
                      item.code,
                      `The output of a suggestion should differ from the original source code for suggestion at index: ${index} on error with message: "${message.message}"`,
                    );
                  },
                );
              } else {
                assert.fail(
                  "Test error object property 'suggestions' should be an array or a number",
                );
              }
            }
          }
        } else {
          // Message was an unexpected type
          assert.fail(
            `Error should be a string, object, or RegExp, but found (${util.inspect(
              message,
            )})`,
          );
        }
      }
    }

    if (hasOwnProperty(item, 'output')) {
      if (item.output == null) {
        if (result.outputs.length) {
          assert.strictEqual(
            result.outputs[0],
            item.code,
            'Expected no autofixes to be suggested.',
          );
        }
      } else if (typeof item.output === 'string') {
        assert(result.outputs.length > 0, 'Expected autofix to be suggested.');
        assert.strictEqual(
          result.outputs[0],
          item.output,
          'Output is incorrect.',
        );
        if (result.outputs.length) {
          assert.deepStrictEqual(
            result.outputs,
            [item.output],
            'Multiple autofixes are required due to overlapping fix ranges - please use the array form of output to declare all of the expected autofix passes.',
          );
        }
      } else {
        assert(result.outputs.length > 0, 'Expected autofix to be suggested.');
        assert.deepStrictEqual(
          result.outputs,
          item.output,
          'Outputs do not match.',
        );
      }
    } else if (result.outputs.length) {
      assert.strictEqual(
        result.outputs[0],
        item.code,
        "The rule fixed the code. Please add 'output' property.",
      );
    }

    assertASTDidntChange(result.beforeAST, result.afterAST);
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Check if the template is invalid or not
   * all invalid cases go through this.
   */
```

- **Parameters**:
  - `ruleName: string`
  - `rule: RuleModule<MessageIds, Options>`
  - `item: InvalidTestCase<MessageIds, Options>`
  - `seenInvalidTestCases: Set<string>`
- **Return Type**: `void`
- **Calls**:
  - `assert.ok`
  - `Array.isArray`
  - `assert.fail`
  - `checkDuplicateTestCase`
  - `hasOwnProperty (from ./utils/hasOwnProperty)`
  - `Object.keys(rule.meta.messages)
          .map(key => `'${key}'`)
          .join`
  - `this.runRuleForItem`
  - `result.messages.map`
  - `message.ruleId.startsWith`
  - `message.ruleId.slice`
  - `seenMessageIndices.get`
  - `seenMessageIndices.has`
  - `seenMessageIndices.set`
  - `assert.strictEqual`
  - `util.format`
  - `util.inspect`
  - `messages.some`
  - `assert (from node:assert)`
  - `assertMessageMatches`
  - `Object.keys(error).forEach`
  - `ERROR_OBJECT_PARAMETERS.has`
  - `getUnsubstitutedMessagePlaceholders`
  - `unsubstitutedPlaceholders.map(name => `'${name}'`).join`
  - `interpolate (from ./utils/interpolate)`
  - `Boolean`
  - `error.suggestions.forEach`
  - `Object.keys(expectedSuggestion).forEach`
  - `SUGGESTION_OBJECT_PARAMETERS.has`
  - `SourceCodeFixer.applyFixes`
  - `this.#getLinterForFilename(
                      item.filename,
                    )
                      .verify(
                        codeWithAppliedSuggestion,
                        omitCustomConfigProperties(result.config),
                        result.filename,
                      )
                      .find`
  - `[
                        'A fatal parsing error occurred in suggestion fix.',
                        `Error: ${errorMessageInSuggestion?.message}`,
                        'Suggestion output:',
                        codeWithAppliedSuggestion,
                      ].join`
  - `assert.notStrictEqual`
  - `assert.deepStrictEqual`
  - `assertASTDidntChange`
- **Internal Comments**:
```
// console.log({ messages });
// Just an error message. (x3)
/*
           * Error object.
           * This may have a message, messageId, data, node type, line, and/or
           * column.
           */ (x6)
// @ts-expect-error -- we purposely don't define `message` on our types as the current standard is `messageId` (x4)
/*
               *  if data was provided, then directly compare the returned message to a synthetic
               *  interpolated message using the same message ID and data provided in the test.
               *  See https://github.com/eslint/eslint/issues/9890 for context.
               */ (x2)
// Support asserting there are no suggestions (x2)
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
// It is possible that error.suggestions is a number (x2)
// eslint-disable-next-line @typescript-eslint/restrict-template-expressions (x2)
// @ts-expect-error -- we purposely don't define `desc` on our types as the current standard is `messageId` (x3)
// Verify if suggestion fix makes a syntax error or not. (x2)
// Message was an unexpected type (x4)
```

### `getFilename(originalFilename: string | undefined, testOptions: ParserOptions | undefined): string`

<details><summary>Code</summary>

```ts
(
      originalFilename: string | undefined,
      testOptions: ParserOptions | undefined,
    ): string => {
      const resolvedOptions = deepMerge(
        this.#testerConfig.languageOptions.parserOptions,
        testOptions,
      ) as ParserOptions;
      const filename =
        originalFilename ??
        (resolvedOptions.ecmaFeatures?.jsx
          ? this.#testerConfig.defaultFilenames.tsx
          : this.#testerConfig.defaultFilenames.ts);
      if (resolvedOptions.project) {
        return path.join(
          resolvedOptions.tsconfigRootDir ?? process.cwd(),
          filename,
        );
      }
      return filename;
    }
```
</details>

- **Parameters**:
  - `originalFilename: string | undefined`
  - `testOptions: ParserOptions | undefined`
- **Return Type**: `string`
- **Calls**:
  - `deepMerge (from @typescript-eslint/utils/eslint-utils)`
  - `path.join`
  - `process.cwd`
### `normalizeTest(test: T): T`

<details><summary>Code</summary>

```ts
<
      MessageIds extends string,
      Options extends readonly unknown[],
      T extends InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
    >(
      test: T,
    ): T => {
      const { languageOptions = {} } = test;
      if (languageOptions.parser === parser) {
        throw new Error(DUPLICATE_PARSER_ERROR_MESSAGE);
      }
      return {
        ...test,
        filename: getFilename(test.filename, languageOptions.parserOptions),
        languageOptions: {
          ...languageOptions,
          parserOptions: {
            // Re-running simulates --fix mode, which implies an isolated program
            // (i.e. parseAndGenerateServicesCalls[test.filename] > 1).
            disallowAutomaticSingleRunInference: true,
            ...languageOptions.parserOptions,
          },
        },
      };
    }
```
</details>

- **Parameters**:
  - `test: T`
- **Return Type**: `T`
- **Calls**:
  - `getFilename`
- **Internal Comments**:
```
// Re-running simulates --fix mode, which implies an isolated program (x2)
// (i.e. parseAndGenerateServicesCalls[test.filename] > 1). (x2)
```

### `maybeMarkAsOnly(test: T): T`

<details><summary>Code</summary>

```ts
<
      T extends InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
    >(
      test: T,
    ): T => {
      return {
        ...test,
        skip: !satisfiesAllDependencyConstraints(test.dependencyConstraints),
      };
    }
```
</details>

- **Parameters**:
  - `test: T`
- **Return Type**: `T`
- **Calls**:
  - `satisfiesAllDependencyConstraints (from ./utils/dependencyConstraints)`
### `getTestMethod(test: ValidTestCase<TSUtils.NoInfer<Options>>): 'it' | 'itOnly' | 'itSkip'`

<details><summary>Code</summary>

```ts
function getTestMethod(
      test: ValidTestCase<TSUtils.NoInfer<Options>>,
    ): 'it' | 'itOnly' | 'itSkip' {
      if (test.skip) {
        return 'itSkip';
      }
      if (test.only) {
        return 'itOnly';
      }
      return 'it';
    }
```
</details>

- **Parameters**:
  - `test: ValidTestCase<TSUtils.NoInfer<Options>>`
- **Return Type**: `'it' | 'itOnly' | 'itSkip'`
### `assertASTDidntChange(beforeAST: unknown, afterAST: unknown): void`

<details><summary>Code</summary>

```ts
function assertASTDidntChange(beforeAST: unknown, afterAST: unknown): void {
  assert.deepStrictEqual(beforeAST, afterAST, 'Rule should not modify AST.');
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if the AST was changed
 */
```

- **Parameters**:
  - `beforeAST: unknown`
  - `afterAST: unknown`
- **Return Type**: `void`
- **Calls**:
  - `assert.deepStrictEqual`
### `checkDuplicateTestCase(item: unknown, seenTestCases: Set<unknown>): void`

<details><summary>Code</summary>

```ts
function checkDuplicateTestCase(
  item: unknown,
  seenTestCases: Set<unknown>,
): void {
  if (!isSerializable(item)) {
    /*
     * If we can't serialize a test case (because it contains a function, RegExp, etc), skip the check.
     * This might happen with properties like: options, plugins, settings, languageOptions.parser, languageOptions.parserOptions.
     */
    return;
  }

  const serializedTestCase = stringify(item);

  assert(
    !seenTestCases.has(serializedTestCase),
    'detected duplicate test case',
  );
  seenTestCases.add(serializedTestCase);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if this test case is a duplicate of one we have seen before.
 */
```

- **Parameters**:
  - `item: unknown`
  - `seenTestCases: Set<unknown>`
- **Return Type**: `void`
- **Calls**:
  - `isSerializable (from ./utils/serialization)`
  - `stringify (from json-stable-stringify-without-jsonify)`
  - `assert (from node:assert)`
  - `seenTestCases.has`
  - `seenTestCases.add`
- **Internal Comments**:
```
/*
     * If we can't serialize a test case (because it contains a function, RegExp, etc), skip the check.
     * This might happen with properties like: options, plugins, settings, languageOptions.parser, languageOptions.parserOptions.
     */
```

### `assertMessageMatches(actual: string, expected: string | RegExp): void`

<details><summary>Code</summary>

```ts
function assertMessageMatches(actual: string, expected: string | RegExp): void {
  if (expected instanceof RegExp) {
    // assert.js doesn't have a built-in RegExp match function
    assert.ok(
      expected.test(actual),
      `Expected '${actual}' to match ${expected}`,
    );
  } else {
    assert.strictEqual(actual, expected);
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Asserts that the message matches its expected value. If the expected
 * value is a regular expression, it is checked against the actual
 * value.
 */
```

- **Parameters**:
  - `actual: string`
  - `expected: string | RegExp`
- **Return Type**: `void`
- **Calls**:
  - `assert.ok`
  - `expected.test`
  - `assert.strictEqual`
- **Internal Comments**:
```
// assert.js doesn't have a built-in RegExp match function (x4)
```


---

## Classes

### `RuleTester`

<details><summary>Class Code</summary>

```ts
export class RuleTester extends TestFramework {
  readonly #lintersByBasePath: Map<string | undefined, Linter>;
  readonly #rules: Record<string, AnyRuleCreateFunction | AnyRuleModule> = {};
  readonly #testerConfig: TesterConfigWithDefaults;

  /**
   * Creates a new instance of RuleTester.
   */
  constructor(testerConfig?: RuleTesterConfig) {
    super();

    /**
     * The configuration to use for this tester. Combination of the tester
     * configuration and the default configuration.
     */
    this.#testerConfig = merge({}, defaultConfig, testerConfig, {
      rules: { [`${RULE_TESTER_PLUGIN_PREFIX}validate-ast`]: 'error' },
    });

    this.#lintersByBasePath = new Map();

    // make sure that the parser doesn't hold onto file handles between tests
    // on linux (i.e. our CI env), there can be very a limited number of watch handles available
    const constructor = this.constructor as typeof RuleTester;
    constructor.afterAll(() => {
      try {
        defaultParser.clearCaches();
      } catch {
        // ignored on purpose
      }
    });
  }

  #getLinterForFilename(filename: string | undefined): Linter {
    let basePath: string | undefined =
      this.#testerConfig.languageOptions.parserOptions?.tsconfigRootDir;
    // For an absolute path (`/foo.ts`), or a path that steps
    // up (`../foo.ts`), resolve the path relative to the base
    // path (using the current working directory if the parser
    // options did not specify a base path) and use the file's
    // root as the base path so that the file is under the base
    // path. For any other path, which would just be a plain
    // file name (`foo.ts`), don't change the base path.
    if (
      filename != null &&
      (path.isAbsolute(filename) || filename.startsWith('..'))
    ) {
      basePath = path.parse(
        path.resolve(basePath ?? process.cwd(), filename),
      ).root;
    }

    let linterForBasePath = this.#lintersByBasePath.get(basePath);
    if (!linterForBasePath) {
      linterForBasePath = (() => {
        const linter = new Linter({
          configType: 'flat',
          cwd: basePath,
        });

        // This nonsense is a workaround for https://github.com/jestjs/jest/issues/14840
        // see also https://github.com/typescript-eslint/typescript-eslint/issues/8942
        //
        // For some reason rethrowing exceptions skirts around the circular JSON error.
        const oldVerify = linter.verify.bind(linter);
        linter.verify = (
          ...args: Parameters<Linter['verify']>
        ): ReturnType<Linter['verify']> => {
          try {
            return oldVerify(...args);
          } catch (error) {
            throw new Error('Caught an error while linting', {
              cause: error,
            });
          }
        };

        return linter;
      })();
      this.#lintersByBasePath.set(basePath, linterForBasePath);
    }
    return linterForBasePath;
  }

  /**
   * Set the configuration to use for all future tests
   */
  static setDefaultConfig(config: RuleTesterConfig): void {
    if (typeof config !== 'object' || config == null) {
      throw new TypeError(
        'RuleTester.setDefaultConfig: config must be an object',
      );
    }
    // Make sure the rules object exists since it is assumed to exist later
    defaultConfig = deepMerge(
      defaultConfig,
      // @ts-expect-error -- no index signature
      config,
    ) as TesterConfigWithDefaults;
  }

  /**
   * Get the current configuration used for all tests
   */
  static getDefaultConfig(): Readonly<RuleTesterConfig> {
    return defaultConfig;
  }

  /**
   * Reset the configuration to the initial configuration of the tester removing
   * any changes made until now.
   */
  static resetDefaultConfig(): void {
    defaultConfig = merge({}, testerDefaultConfig);
  }

  /**
   * Adds the `only` property to a test to run it in isolation.
   */
  static only<Options extends readonly unknown[]>(
    item: string | ValidTestCase<Options>,
  ): ValidTestCase<Options>;
  /**
   * Adds the `only` property to a test to run it in isolation.
   */
  static only<MessageIds extends string, Options extends readonly unknown[]>(
    item: InvalidTestCase<MessageIds, Options>,
  ): InvalidTestCase<MessageIds, Options>;
  static only<MessageIds extends string, Options extends readonly unknown[]>(
    item:
      | string
      | InvalidTestCase<MessageIds, Options>
      | ValidTestCase<Options>,
  ): InvalidTestCase<MessageIds, Options> | ValidTestCase<Options> {
    if (typeof item === 'string') {
      return { code: item, only: true };
    }

    return { ...item, only: true };
  }

  /**
   * Define a rule for one particular run of tests.
   */
  #normalizeTests<
    MessageIds extends string,
    Options extends readonly unknown[],
  >(
    rawTests: RunTests<MessageIds, Options>,
  ): NormalizedRunTests<MessageIds, Options> {
    /*
    Automatically add a filename to the tests to enable type-aware tests to "just work".
    This saves users having to verbosely and manually add the filename to every
    single test case.
    Hugely helps with the string-based valid test cases as it means they don't
    need to be made objects!
    */
    const getFilename = (
      originalFilename: string | undefined,
      testOptions: ParserOptions | undefined,
    ): string => {
      const resolvedOptions = deepMerge(
        this.#testerConfig.languageOptions.parserOptions,
        testOptions,
      ) as ParserOptions;
      const filename =
        originalFilename ??
        (resolvedOptions.ecmaFeatures?.jsx
          ? this.#testerConfig.defaultFilenames.tsx
          : this.#testerConfig.defaultFilenames.ts);
      if (resolvedOptions.project) {
        return path.join(
          resolvedOptions.tsconfigRootDir ?? process.cwd(),
          filename,
        );
      }
      return filename;
    };
    const normalizeTest = <
      MessageIds extends string,
      Options extends readonly unknown[],
      T extends InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
    >(
      test: T,
    ): T => {
      const { languageOptions = {} } = test;
      if (languageOptions.parser === parser) {
        throw new Error(DUPLICATE_PARSER_ERROR_MESSAGE);
      }
      return {
        ...test,
        filename: getFilename(test.filename, languageOptions.parserOptions),
        languageOptions: {
          ...languageOptions,
          parserOptions: {
            // Re-running simulates --fix mode, which implies an isolated program
            // (i.e. parseAndGenerateServicesCalls[test.filename] > 1).
            disallowAutomaticSingleRunInference: true,
            ...languageOptions.parserOptions,
          },
        },
      };
    };

    const normalizedTests = {
      invalid: rawTests.invalid.map(normalizeTest),
      valid: rawTests.valid
        .map(test => {
          if (typeof test === 'string') {
            return { code: test };
          }
          return test;
        })
        .map(normalizeTest),
    };

    // convenience iterator to make it easy to loop all tests without a concat
    const allTestsIterator = {
      *[Symbol.iterator](): Generator<ValidTestCase<Options>, void> {
        for (const testCase of normalizedTests.valid) {
          yield testCase;
        }
        for (const testCase of normalizedTests.invalid) {
          yield testCase;
        }
      },
    };

    const hasOnly = ((): boolean => {
      for (const test of allTestsIterator) {
        if (test.only) {
          return true;
        }
      }
      return false;
    })();
    if (hasOnly) {
      // if there is an `only: true` - don't try apply constraints - assume that
      // we are in "local development" mode rather than "CI validation" mode
      return normalizedTests;
    }

    const hasConstraints = ((): boolean => {
      for (const test of allTestsIterator) {
        if (
          test.dependencyConstraints &&
          Object.keys(test.dependencyConstraints).length > 0
        ) {
          return true;
        }
      }
      return false;
    })();
    if (!hasConstraints) {
      return normalizedTests;
    }

    /*
    Mark all unsatisfactory tests as `skip: true`.
    We do this instead of just omitting the tests entirely because it gives the
    test framework the opportunity to log the test as skipped rather than the test
    just disappearing without a trace.
    */
    const maybeMarkAsOnly = <
      T extends InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
    >(
      test: T,
    ): T => {
      return {
        ...test,
        skip: !satisfiesAllDependencyConstraints(test.dependencyConstraints),
      };
    };
    normalizedTests.valid = normalizedTests.valid.map(maybeMarkAsOnly);
    normalizedTests.invalid = normalizedTests.invalid.map(maybeMarkAsOnly);

    return normalizedTests;
  }

  defineRule(name: string, rule: AnyRuleModule): void {
    this.#rules[name] = {
      ...rule,
      // Create a wrapper rule that freezes the `context` properties.
      create(context): RuleListener {
        freezeDeeply(context.options);
        freezeDeeply(context.settings);
        freezeDeeply(context.parserOptions);

        return (typeof rule === 'function' ? rule : rule.create)(context);
      },
    };
  }

  /**
   * Runs a hook on the given item when it's assigned to the given property
   * @throws {Error} If the property is not a function or that function throws an error
   */
  #runHook<MessageIds extends string, Options extends readonly unknown[]>(
    item: InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
    prop: keyof Pick<typeof item, 'after' | 'before'>,
  ): void {
    if (hasOwnProperty(item, prop)) {
      assert.strictEqual(
        typeof item[prop],
        'function',
        `Optional test case property '${prop}' must be a function`,
      );
      item[prop]();
    }
  }

  /**
   * Adds a new rule test to execute.
   */
  run<MessageIds extends string, Options extends readonly unknown[]>(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    test: RunTests<TSUtils.NoInfer<MessageIds>, TSUtils.NoInfer<Options>>,
  ): void {
    const constructor = this.constructor as typeof RuleTester;

    if (
      this.#testerConfig.dependencyConstraints &&
      !satisfiesAllDependencyConstraints(
        this.#testerConfig.dependencyConstraints,
      )
    ) {
      // for frameworks like mocha or jest that have a "skip" version of their function
      // we can provide a nice skipped test!
      constructor.describeSkip(ruleName, () => {
        constructor.it(
          'All tests skipped due to unsatisfied constructor dependency constraints',
          () => {
            // some frameworks error if there are no assertions
            assert.equal(true, true);
          },
        );
      });

      // don't run any tests because we don't match the base constraint
      return;
    }

    if (!test || typeof test !== 'object') {
      throw new TypeError(
        `Test Scenarios for rule ${ruleName} : Could not find test scenario object`,
      );
    }

    const scenarioErrors: string[] = [];
    REQUIRED_SCENARIOS.forEach(scenarioType => {
      if (!test[scenarioType]) {
        scenarioErrors.push(
          `Could not find any ${scenarioType} test scenarios`,
        );
      }
    });

    if (scenarioErrors.length > 0) {
      throw new Error(
        [
          `Test Scenarios for rule ${ruleName} is invalid:`,
          ...scenarioErrors,
        ].join('\n'),
      );
    }

    const seenValidTestCases = new Set<string>();
    const seenInvalidTestCases = new Set<string>();
    const normalizedTests = this.#normalizeTests(test);

    function getTestMethod(
      test: ValidTestCase<TSUtils.NoInfer<Options>>,
    ): 'it' | 'itOnly' | 'itSkip' {
      if (test.skip) {
        return 'itSkip';
      }
      if (test.only) {
        return 'itOnly';
      }
      return 'it';
    }

    /*
     * This creates a test suite and pipes all supplied info through
     * one of the templates above.
     */
    constructor.describe(ruleName, () => {
      if (normalizedTests.valid.length) {
        constructor.describe('valid', () => {
          normalizedTests.valid.forEach(valid => {
            const testName = ((): string => {
              if (valid.name == null || valid.name.length === 0) {
                return valid.code;
              }
              return valid.name;
            })();
            constructor[getTestMethod(valid)](sanitize(testName), () => {
              try {
                this.#runHook(valid, 'before');
                this.#testValidTemplate(
                  ruleName,
                  rule,
                  valid,
                  seenValidTestCases,
                );
              } finally {
                this.#runHook(valid, 'after');
              }
            });
          });
        });
      }

      if (normalizedTests.invalid.length) {
        constructor.describe('invalid', () => {
          normalizedTests.invalid.forEach(invalid => {
            const name = ((): string => {
              if (invalid.name == null || invalid.name.length === 0) {
                return invalid.code;
              }
              return invalid.name;
            })();
            constructor[getTestMethod(invalid)](sanitize(name), () => {
              try {
                this.#runHook(invalid, 'before');
                this.#testInvalidTemplate(
                  ruleName,
                  rule,
                  // no need to pass no infer type parameter down to private methods
                  invalid as InvalidTestCase<MessageIds, Options>,
                  seenInvalidTestCases,
                );
              } finally {
                this.#runHook(invalid, 'after');
              }
            });
          });
        });
      }
    });
  }

  /**
   * Run the rule for the given item
   * @throws {Error} If an invalid schema.
   * Use @private instead of #private to expose it for testing purposes
   */
  private runRuleForItem<
    MessageIds extends string,
    Options extends readonly unknown[],
  >(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    item: InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
  ): {
    afterAST: TSESTree.Program;
    beforeAST: TSESTree.Program;
    config: RuleTesterConfig;
    filename?: string;
    messages: Linter.LintMessage[];
    outputs: string[];
  } {
    this.defineRule(ruleName, rule);

    let config: TesterConfigWithDefaults = merge({}, this.#testerConfig, {
      files: ['**'],
      plugins: {
        [RULE_TESTER_PLUGIN]: {
          rules: {
            /**
             * Setup AST getters.
             * The goal is to check whether or not AST was modified when
             * running the rule under test.
             */
            'validate-ast': {
              create(): RuleListener {
                return {
                  Program(node: TSESTree.Program): void {
                    beforeAST = cloneDeeplyExcludesParent(node);
                  },
                  'Program:exit'(node: TSESTree.Program): void {
                    afterAST = node;
                  },
                };
              },
            },
            ...this.#rules,
          },
        },
      },
    });

    // Unlike other properties, we don't want to spread props between different parsers.
    config.languageOptions.parser =
      item.languageOptions?.parser ?? this.#testerConfig.languageOptions.parser;

    let code;
    let filename;
    let beforeAST: TSESTree.Program;
    let afterAST: TSESTree.Program;

    if (typeof item === 'string') {
      code = item;
    } else {
      code = item.code;

      /*
       * Assumes everything on the item is a config except for the
       * parameters used by this tester
       */
      const itemConfig: Record<string, unknown> = { ...item };

      for (const parameter of RULE_TESTER_PARAMETERS) {
        // eslint-disable-next-line @typescript-eslint/no-dynamic-delete
        delete itemConfig[parameter];
      }

      /*
       * Create the config object from the tester config and this item
       * specific configurations.
       */
      config = merge(config, itemConfig);
    }

    if (hasOwnProperty(item, 'only')) {
      assert.ok(
        typeof item.only === 'boolean',
        "Optional test case property 'only' must be a boolean",
      );
    }
    if (hasOwnProperty(item, 'filename')) {
      assert.ok(
        typeof item.filename === 'string',
        "Optional test case property 'filename' must be a string",
      );
      filename = item.filename;
    }

    const prefixedRuleName = `${RULE_TESTER_PLUGIN_PREFIX}${ruleName}`;

    if (hasOwnProperty(item, 'options')) {
      assert(Array.isArray(item.options), 'options must be an array');
      config.rules[prefixedRuleName] = ['error', ...item.options];
    } else {
      config.rules[prefixedRuleName] = 'error';
    }

    config.languageOptions ??= {};
    config.languageOptions.parser ??= defaultParser;
    config.languageOptions.parser = wrapParser(config.languageOptions.parser);

    const schema = getRuleOptionsSchema(rule);

    if (schema) {
      ajv.validateSchema(schema);

      if (ajv.errors) {
        const errors = ajv.errors
          .map(error => {
            const field =
              error.dataPath[0] === '.'
                ? error.dataPath.slice(1)
                : error.dataPath;

            return `\t${field}: ${error.message}`;
          })
          .join('\n');

        throw new Error(
          [`Schema for rule ${ruleName} is invalid:`, errors].join(
            // no space after comma to match eslint core
            ',',
          ),
        );
      }

      /*
       * `ajv.validateSchema` checks for errors in the structure of the schema (by comparing the schema against a "meta-schema"),
       * and it reports those errors individually. However, there are other types of schema errors that only occur when compiling
       * the schema (e.g. using invalid defaults in a schema), and only one of these errors can be reported at a time. As a result,
       * the schema is compiled here separately from checking for `validateSchema` errors.
       */
      try {
        ajv.compile(schema);
      } catch (err) {
        throw new Error(
          `Schema for rule ${ruleName} is invalid: ${(err as Error).message}`,
        );
      }
    }

    validate(config, RULE_TESTER_PLUGIN, id => (id === ruleName ? rule : null));

    // Verify the code.
    let initialMessages: Linter.LintMessage[] | null = null;
    let messages: Linter.LintMessage[] | null = null;
    let fixedResult: SourceCodeFixer.AppliedFixes | null = null;
    let passNumber = 0;
    const outputs: string[] = [];
    const configWithoutCustomKeys = omitCustomConfigProperties(config);
    const linter = this.#getLinterForFilename(filename);

    do {
      passNumber++;

      const SourceCodePrototype = SourceCode.prototype as Record<
        ForbiddenMethodName,
        ForbiddenFunction
      >;

      const { applyInlineConfig, applyLanguageOptions, finalize } =
        SourceCodePrototype;

      try {
        forbiddenMethods.forEach(methodName => {
          SourceCodePrototype[methodName] = throwForbiddenMethodError(
            methodName,
            SourceCodePrototype,
          );
        });

        const actualConfig = merge(configWithoutCustomKeys, {
          languageOptions: {
            ...configWithoutCustomKeys.languageOptions,
            parserOptions: {
              ecmaVersion: 'latest',
              sourceType: 'module',
              ...configWithoutCustomKeys.languageOptions?.parserOptions,
            },
          },
          linterOptions: {
            reportUnusedDisableDirectives: 1,
            ...configWithoutCustomKeys.linterOptions,
          },
        });
        messages = linter.verify(code, actualConfig, filename);
      } finally {
        SourceCodePrototype.applyInlineConfig = applyInlineConfig;
        SourceCodePrototype.applyLanguageOptions = applyLanguageOptions;
        SourceCodePrototype.finalize = finalize;
      }

      initialMessages ??= messages;

      if (messages.length === 0) {
        break;
      }

      const fatalErrorMessage = messages.find(m => m.fatal);
      assert(
        !fatalErrorMessage,
        `A fatal parsing error occurred: ${fatalErrorMessage?.message}`,
      );

      fixedResult = SourceCodeFixer.applyFixes(code, messages);
      if (fixedResult.output === code) {
        break;
      }
      code = fixedResult.output;
      outputs.push(code);

      // Verify if autofix makes a syntax error or not.
      const errorMessageInFix = linter
        .verify(fixedResult.output, configWithoutCustomKeys, filename)
        .find(m => m.fatal);

      assert(
        !errorMessageInFix,
        [
          'A fatal parsing error occurred in autofix.',
          `Error: ${errorMessageInFix?.message}`,
          'Autofix output:',
          fixedResult.output,
        ].join('\n'),
      );
    } while (fixedResult.fixed && passNumber < 10);

    return {
      config,
      filename,
      messages: initialMessages,
      outputs,
      // is definitely assigned within the `@rule-tester/validate-ast` rule
      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      beforeAST: beforeAST!,
      // is definitely assigned within the `@rule-tester/validate-ast` rule
      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      afterAST: cloneDeeplyExcludesParent(afterAST!),
    };
  }

  /**
   * Check if the template is valid or not
   * all valid cases go through this
   */
  #testValidTemplate<
    MessageIds extends string,
    Options extends readonly unknown[],
  >(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    itemIn: string | ValidTestCase<Options>,
    seenValidTestCases: Set<string>,
  ): void {
    const item: ValidTestCase<Options> =
      typeof itemIn === 'object' ? itemIn : { code: itemIn };

    assert.ok(
      typeof item.code === 'string',
      "Test case must specify a string value for 'code'",
    );
    if (item.name) {
      assert.ok(
        typeof item.name === 'string',
        "Optional test case property 'name' must be a string",
      );
    }

    checkDuplicateTestCase(item, seenValidTestCases);

    const result = this.runRuleForItem(ruleName, rule, item);
    const messages = result.messages;

    assert.strictEqual(
      messages.length,
      0,
      util.format(
        'Should have no errors but had %d: %s',
        messages.length,
        util.inspect(messages),
      ),
    );

    assertASTDidntChange(result.beforeAST, result.afterAST);
  }

  /**
   * Check if the template is invalid or not
   * all invalid cases go through this.
   */
  #testInvalidTemplate<
    MessageIds extends string,
    Options extends readonly unknown[],
  >(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    item: InvalidTestCase<MessageIds, Options>,
    seenInvalidTestCases: Set<string>,
  ): void {
    assert.ok(
      typeof item.code === 'string',
      "Test case must specify a string value for 'code'",
    );
    if (item.name) {
      assert.ok(
        typeof item.name === 'string',
        "Optional test case property 'name' must be a string",
      );
    }
    assert.ok(
      item.errors || item.errors === 0,
      `Did not specify errors for an invalid test of ${ruleName}`,
    );

    if (Array.isArray(item.errors) && item.errors.length === 0) {
      assert.fail('Invalid cases must have at least one error');
    }

    checkDuplicateTestCase(item, seenInvalidTestCases);

    const ruleHasMetaMessages =
      hasOwnProperty(rule, 'meta') && hasOwnProperty(rule.meta, 'messages');
    const friendlyIDList = ruleHasMetaMessages
      ? `[${Object.keys(rule.meta.messages)
          .map(key => `'${key}'`)
          .join(', ')}]`
      : null;

    const result = this.runRuleForItem(ruleName, rule, item);
    const messages = result.messages.map(message => ({
      ...message,
      ...(message.ruleId && {
        ruleId: message.ruleId.startsWith(RULE_TESTER_PLUGIN_PREFIX)
          ? message.ruleId.slice(RULE_TESTER_PLUGIN_PREFIX.length)
          : message.ruleId,
      }),
    }));

    for (const message of messages) {
      if (hasOwnProperty(message, 'suggestions')) {
        const seenMessageIndices = new Map<string, number>();

        for (let i = 0; i < message.suggestions.length; i += 1) {
          const suggestionMessage = message.suggestions[i].desc;
          const previous = seenMessageIndices.get(suggestionMessage);

          assert.ok(
            !seenMessageIndices.has(suggestionMessage),
            `Suggestion message '${suggestionMessage}' reported from suggestion ${i} was previously reported by suggestion ${previous}. Suggestion messages should be unique within an error.`,
          );
          seenMessageIndices.set(suggestionMessage, i);
        }
      }
    }

    if (typeof item.errors === 'number') {
      if (item.errors === 0) {
        assert.fail("Invalid cases must have 'error' value greater than 0");
      }

      assert.strictEqual(
        messages.length,
        item.errors,
        util.format(
          'Should have %d error%s but had %d: %s',
          item.errors,
          item.errors === 1 ? '' : 's',
          messages.length,
          util.inspect(messages),
        ),
      );
    } else {
      assert.strictEqual(
        messages.length,
        item.errors.length,
        util.format(
          'Should have %d error%s but had %d: %s',
          item.errors.length,
          item.errors.length === 1 ? '' : 's',
          messages.length,
          util.inspect(messages),
        ),
      );

      const hasMessageOfThisRule = messages.some(m => m.ruleId === ruleName);

      // console.log({ messages });
      for (let i = 0, l = item.errors.length; i < l; i++) {
        const error = item.errors[i];
        const message = messages[i];

        assert(
          hasMessageOfThisRule,
          'Error rule name should be the same as the name of the rule being tested',
        );

        if (typeof error === 'string' || error instanceof RegExp) {
          // Just an error message.
          assertMessageMatches(message.message, error);
          assert.ok(
            message.suggestions == null,
            `Error at index ${i} has suggestions. Please convert the test error into an object and specify 'suggestions' property on it to test suggestions.`,
          );
        } else if (typeof error === 'object' && error != null) {
          /*
           * Error object.
           * This may have a message, messageId, data, node type, line, and/or
           * column.
           */

          Object.keys(error).forEach(propertyName => {
            assert.ok(
              ERROR_OBJECT_PARAMETERS.has(propertyName),
              `Invalid error property name '${propertyName}'. Expected one of ${FRIENDLY_ERROR_OBJECT_PARAMETER_LIST}.`,
            );
          });

          // @ts-expect-error -- we purposely don't define `message` on our types as the current standard is `messageId`
          if (hasOwnProperty(error, 'message')) {
            assert.ok(
              !hasOwnProperty(error, 'messageId'),
              "Error should not specify both 'message' and a 'messageId'.",
            );
            assert.ok(
              !hasOwnProperty(error, 'data'),
              "Error should not specify both 'data' and 'message'.",
            );
            assertMessageMatches(
              message.message,
              // @ts-expect-error -- we purposely don't define `message` on our types as the current standard is `messageId`
              error.message as unknown,
            );
          } else if (hasOwnProperty(error, 'messageId')) {
            assert.ok(
              ruleHasMetaMessages,
              "Error can not use 'messageId' if rule under test doesn't define 'meta.messages'.",
            );
            if (!hasOwnProperty(rule.meta.messages, error.messageId)) {
              assert(
                false,
                `Invalid messageId '${error.messageId}'. Expected one of ${friendlyIDList}.`,
              );
            }
            assert.strictEqual(
              message.messageId,
              error.messageId,
              `messageId '${message.messageId}' does not match expected messageId '${error.messageId}'.`,
            );

            const unsubstitutedPlaceholders =
              getUnsubstitutedMessagePlaceholders(
                message.message,
                rule.meta.messages[message.messageId],
                error.data,
              );

            assert.ok(
              unsubstitutedPlaceholders.length === 0,
              `The reported message has ${unsubstitutedPlaceholders.length > 1 ? `unsubstituted placeholders: ${unsubstitutedPlaceholders.map(name => `'${name}'`).join(', ')}` : `an unsubstituted placeholder '${unsubstitutedPlaceholders[0]}'`}. Please provide the missing ${unsubstitutedPlaceholders.length > 1 ? 'values' : 'value'} via the 'data' property in the context.report() call.`,
            );

            if (hasOwnProperty(error, 'data')) {
              /*
               *  if data was provided, then directly compare the returned message to a synthetic
               *  interpolated message using the same message ID and data provided in the test.
               *  See https://github.com/eslint/eslint/issues/9890 for context.
               */
              const unformattedOriginalMessage =
                rule.meta.messages[error.messageId];
              const rehydratedMessage = interpolate(
                unformattedOriginalMessage,
                error.data,
              );

              assert.strictEqual(
                message.message,
                rehydratedMessage,
                `Hydrated message "${rehydratedMessage}" does not match "${message.message}"`,
              );
            }
          } else {
            assert.fail(
              "Test error must specify either a 'messageId' or 'message'.",
            );
          }

          if (error.type) {
            assert.strictEqual(
              message.nodeType,
              error.type,
              `Error type should be ${error.type}, found ${message.nodeType}`,
            );
          }

          if (hasOwnProperty(error, 'line')) {
            assert.strictEqual(
              message.line,
              error.line,
              `Error line should be ${error.line}`,
            );
          }

          if (hasOwnProperty(error, 'column')) {
            assert.strictEqual(
              message.column,
              error.column,
              `Error column should be ${error.column}`,
            );
          }

          if (hasOwnProperty(error, 'endLine')) {
            assert.strictEqual(
              message.endLine,
              error.endLine,
              `Error endLine should be ${error.endLine}`,
            );
          }

          if (hasOwnProperty(error, 'endColumn')) {
            assert.strictEqual(
              message.endColumn,
              error.endColumn,
              `Error endColumn should be ${error.endColumn}`,
            );
          }

          assert.ok(
            !message.suggestions || hasOwnProperty(error, 'suggestions'),
            `Error at index ${i} has suggestions. Please specify 'suggestions' property on the test error object.`,
          );
          if (hasOwnProperty(error, 'suggestions')) {
            // Support asserting there are no suggestions
            const expectsSuggestions = Array.isArray(error.suggestions)
              ? error.suggestions.length > 0
              : Boolean(error.suggestions);
            const hasSuggestions = message.suggestions != null;
            // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
            const messageSuggestions = message.suggestions!;

            if (!hasSuggestions && expectsSuggestions) {
              assert.ok(
                !error.suggestions,
                `Error should have suggestions on error with message: "${message.message}"`,
              );
            } else if (hasSuggestions) {
              assert.ok(
                expectsSuggestions,
                `Error should have no suggestions on error with message: "${message.message}"`,
              );
              if (typeof error.suggestions === 'number') {
                assert.strictEqual(
                  messageSuggestions.length,
                  error.suggestions,
                  // It is possible that error.suggestions is a number
                  // eslint-disable-next-line @typescript-eslint/restrict-template-expressions
                  `Error should have ${error.suggestions} suggestions. Instead found ${messageSuggestions.length} suggestions`,
                );
              } else if (Array.isArray(error.suggestions)) {
                assert.strictEqual(
                  messageSuggestions.length,
                  error.suggestions.length,
                  `Error should have ${error.suggestions.length} suggestions. Instead found ${messageSuggestions.length} suggestions`,
                );

                error.suggestions.forEach(
                  (expectedSuggestion: SuggestionOutput<MessageIds>, index) => {
                    assert.ok(
                      typeof expectedSuggestion === 'object' &&
                        expectedSuggestion != null,
                      "Test suggestion in 'suggestions' array must be an object.",
                    );
                    Object.keys(expectedSuggestion).forEach(propertyName => {
                      assert.ok(
                        SUGGESTION_OBJECT_PARAMETERS.has(propertyName),
                        `Invalid suggestion property name '${propertyName}'. Expected one of ${FRIENDLY_SUGGESTION_OBJECT_PARAMETER_LIST}.`,
                      );
                    });

                    const actualSuggestion = messageSuggestions[index];
                    const suggestionPrefix = `Error Suggestion at index ${index}:`;

                    // @ts-expect-error -- we purposely don't define `desc` on our types as the current standard is `messageId`
                    if (hasOwnProperty(expectedSuggestion, 'desc')) {
                      // @ts-expect-error -- we purposely don't define `desc` on our types as the current standard is `messageId`
                      const expectedDesc = expectedSuggestion.desc as string;

                      assert.ok(
                        !hasOwnProperty(expectedSuggestion, 'data'),
                        `${suggestionPrefix} Test should not specify both 'desc' and 'data'.`,
                      );
                      assert.ok(
                        !hasOwnProperty(expectedSuggestion, 'messageId'),
                        `${suggestionPrefix} Test should not specify both 'desc' and 'messageId'.`,
                      );
                      assert.strictEqual(
                        actualSuggestion.desc,
                        expectedDesc,
                        `${suggestionPrefix} desc should be "${expectedDesc}" but got "${actualSuggestion.desc}" instead.`,
                      );
                    } else if (
                      hasOwnProperty(expectedSuggestion, 'messageId')
                    ) {
                      assert.ok(
                        ruleHasMetaMessages,
                        `${suggestionPrefix} Test can not use 'messageId' if rule under test doesn't define 'meta.messages'.`,
                      );
                      assert.ok(
                        hasOwnProperty(
                          rule.meta.messages,
                          expectedSuggestion.messageId,
                        ),
                        `${suggestionPrefix} Test has invalid messageId '${expectedSuggestion.messageId}', the rule under test allows only one of ${friendlyIDList}.`,
                      );
                      assert.strictEqual(
                        actualSuggestion.messageId,
                        expectedSuggestion.messageId,
                        `${suggestionPrefix} messageId should be '${expectedSuggestion.messageId}' but got '${actualSuggestion.messageId}' instead.`,
                      );

                      const unsubstitutedPlaceholders =
                        getUnsubstitutedMessagePlaceholders(
                          actualSuggestion.desc,
                          rule.meta.messages[expectedSuggestion.messageId],
                          expectedSuggestion.data,
                        );

                      assert.ok(
                        unsubstitutedPlaceholders.length === 0,
                        `The message of the suggestion has ${unsubstitutedPlaceholders.length > 1 ? `unsubstituted placeholders: ${unsubstitutedPlaceholders.map(name => `'${name}'`).join(', ')}` : `an unsubstituted placeholder '${unsubstitutedPlaceholders[0]}'`}. Please provide the missing ${unsubstitutedPlaceholders.length > 1 ? 'values' : 'value'} via the 'data' property for the suggestion in the context.report() call.`,
                      );

                      if (hasOwnProperty(expectedSuggestion, 'data')) {
                        const unformattedMetaMessage =
                          rule.meta.messages[expectedSuggestion.messageId];
                        const rehydratedDesc = interpolate(
                          unformattedMetaMessage,
                          expectedSuggestion.data,
                        );

                        assert.strictEqual(
                          actualSuggestion.desc,
                          rehydratedDesc,
                          `${suggestionPrefix} Hydrated test desc "${rehydratedDesc}" does not match received desc "${actualSuggestion.desc}".`,
                        );
                      }
                    } else if (hasOwnProperty(expectedSuggestion, 'data')) {
                      assert.fail(
                        `${suggestionPrefix} Test must specify 'messageId' if 'data' is used.`,
                      );
                    } else {
                      assert.fail(
                        `${suggestionPrefix} Test must specify either 'messageId' or 'desc'.`,
                      );
                    }

                    assert.ok(
                      hasOwnProperty(expectedSuggestion, 'output'),
                      `${suggestionPrefix} The "output" property is required.`,
                    );
                    const codeWithAppliedSuggestion =
                      SourceCodeFixer.applyFixes(item.code, [
                        actualSuggestion,
                      ]).output;

                    // Verify if suggestion fix makes a syntax error or not.
                    const errorMessageInSuggestion = this.#getLinterForFilename(
                      item.filename,
                    )
                      .verify(
                        codeWithAppliedSuggestion,
                        omitCustomConfigProperties(result.config),
                        result.filename,
                      )
                      .find(m => m.fatal);

                    assert(
                      !errorMessageInSuggestion,
                      [
                        'A fatal parsing error occurred in suggestion fix.',
                        `Error: ${errorMessageInSuggestion?.message}`,
                        'Suggestion output:',
                        codeWithAppliedSuggestion,
                      ].join('\n'),
                    );

                    assert.strictEqual(
                      codeWithAppliedSuggestion,
                      expectedSuggestion.output,
                      `Expected the applied suggestion fix to match the test suggestion output for suggestion at index: ${index} on error with message: "${message.message}"`,
                    );
                    assert.notStrictEqual(
                      expectedSuggestion.output,
                      item.code,
                      `The output of a suggestion should differ from the original source code for suggestion at index: ${index} on error with message: "${message.message}"`,
                    );
                  },
                );
              } else {
                assert.fail(
                  "Test error object property 'suggestions' should be an array or a number",
                );
              }
            }
          }
        } else {
          // Message was an unexpected type
          assert.fail(
            `Error should be a string, object, or RegExp, but found (${util.inspect(
              message,
            )})`,
          );
        }
      }
    }

    if (hasOwnProperty(item, 'output')) {
      if (item.output == null) {
        if (result.outputs.length) {
          assert.strictEqual(
            result.outputs[0],
            item.code,
            'Expected no autofixes to be suggested.',
          );
        }
      } else if (typeof item.output === 'string') {
        assert(result.outputs.length > 0, 'Expected autofix to be suggested.');
        assert.strictEqual(
          result.outputs[0],
          item.output,
          'Output is incorrect.',
        );
        if (result.outputs.length) {
          assert.deepStrictEqual(
            result.outputs,
            [item.output],
            'Multiple autofixes are required due to overlapping fix ranges - please use the array form of output to declare all of the expected autofix passes.',
          );
        }
      } else {
        assert(result.outputs.length > 0, 'Expected autofix to be suggested.');
        assert.deepStrictEqual(
          result.outputs,
          item.output,
          'Outputs do not match.',
        );
      }
    } else if (result.outputs.length) {
      assert.strictEqual(
        result.outputs[0],
        item.code,
        "The rule fixed the code. Please add 'output' property.",
      );
    }

    assertASTDidntChange(result.beforeAST, result.afterAST);
  }
}
```
</details>

#### Methods

##### `#getLinterForFilename(filename: string | undefined): Linter`

<details><summary>Code</summary>

```ts
#getLinterForFilename(filename: string | undefined): Linter {
    let basePath: string | undefined =
      this.#testerConfig.languageOptions.parserOptions?.tsconfigRootDir;
    // For an absolute path (`/foo.ts`), or a path that steps
    // up (`../foo.ts`), resolve the path relative to the base
    // path (using the current working directory if the parser
    // options did not specify a base path) and use the file's
    // root as the base path so that the file is under the base
    // path. For any other path, which would just be a plain
    // file name (`foo.ts`), don't change the base path.
    if (
      filename != null &&
      (path.isAbsolute(filename) || filename.startsWith('..'))
    ) {
      basePath = path.parse(
        path.resolve(basePath ?? process.cwd(), filename),
      ).root;
    }

    let linterForBasePath = this.#lintersByBasePath.get(basePath);
    if (!linterForBasePath) {
      linterForBasePath = (() => {
        const linter = new Linter({
          configType: 'flat',
          cwd: basePath,
        });

        // This nonsense is a workaround for https://github.com/jestjs/jest/issues/14840
        // see also https://github.com/typescript-eslint/typescript-eslint/issues/8942
        //
        // For some reason rethrowing exceptions skirts around the circular JSON error.
        const oldVerify = linter.verify.bind(linter);
        linter.verify = (
          ...args: Parameters<Linter['verify']>
        ): ReturnType<Linter['verify']> => {
          try {
            return oldVerify(...args);
          } catch (error) {
            throw new Error('Caught an error while linting', {
              cause: error,
            });
          }
        };

        return linter;
      })();
      this.#lintersByBasePath.set(basePath, linterForBasePath);
    }
    return linterForBasePath;
  }
```
</details>

##### `setDefaultConfig(config: RuleTesterConfig): void`

<details><summary>Code</summary>

```ts
static setDefaultConfig(config: RuleTesterConfig): void {
    if (typeof config !== 'object' || config == null) {
      throw new TypeError(
        'RuleTester.setDefaultConfig: config must be an object',
      );
    }
    // Make sure the rules object exists since it is assumed to exist later
    defaultConfig = deepMerge(
      defaultConfig,
      // @ts-expect-error -- no index signature
      config,
    ) as TesterConfigWithDefaults;
  }
```
</details>

##### `getDefaultConfig(): Readonly<RuleTesterConfig>`

<details><summary>Code</summary>

```ts
static getDefaultConfig(): Readonly<RuleTesterConfig> {
    return defaultConfig;
  }
```
</details>

##### `resetDefaultConfig(): void`

<details><summary>Code</summary>

```ts
static resetDefaultConfig(): void {
    defaultConfig = merge({}, testerDefaultConfig);
  }
```
</details>

##### `only(item: string | ValidTestCase<Options>): ValidTestCase<Options>`

<details><summary>Code</summary>

```ts
static only<Options extends readonly unknown[]>(
    item: string | ValidTestCase<Options>,
  ): ValidTestCase<Options>;
```
</details>

##### `only(item: InvalidTestCase<MessageIds, Options>): InvalidTestCase<MessageIds, Options>`

<details><summary>Code</summary>

```ts
static only<MessageIds extends string, Options extends readonly unknown[]>(
    item: InvalidTestCase<MessageIds, Options>,
  ): InvalidTestCase<MessageIds, Options>;
```
</details>

##### `only(item: | string
      | InvalidTestCase<MessageIds, Options>
      | ValidTestCase<Options>): InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>`

<details><summary>Code</summary>

```ts
static only<MessageIds extends string, Options extends readonly unknown[]>(
    item:
      | string
      | InvalidTestCase<MessageIds, Options>
      | ValidTestCase<Options>,
  ): InvalidTestCase<MessageIds, Options> | ValidTestCase<Options> {
    if (typeof item === 'string') {
      return { code: item, only: true };
    }

    return { ...item, only: true };
  }
```
</details>

##### `#normalizeTests(rawTests: RunTests<MessageIds, Options>): NormalizedRunTests<MessageIds, Options>`

<details><summary>Code</summary>

```ts
#normalizeTests<
    MessageIds extends string,
    Options extends readonly unknown[],
  >(
    rawTests: RunTests<MessageIds, Options>,
  ): NormalizedRunTests<MessageIds, Options> {
    /*
    Automatically add a filename to the tests to enable type-aware tests to "just work".
    This saves users having to verbosely and manually add the filename to every
    single test case.
    Hugely helps with the string-based valid test cases as it means they don't
    need to be made objects!
    */
    const getFilename = (
      originalFilename: string | undefined,
      testOptions: ParserOptions | undefined,
    ): string => {
      const resolvedOptions = deepMerge(
        this.#testerConfig.languageOptions.parserOptions,
        testOptions,
      ) as ParserOptions;
      const filename =
        originalFilename ??
        (resolvedOptions.ecmaFeatures?.jsx
          ? this.#testerConfig.defaultFilenames.tsx
          : this.#testerConfig.defaultFilenames.ts);
      if (resolvedOptions.project) {
        return path.join(
          resolvedOptions.tsconfigRootDir ?? process.cwd(),
          filename,
        );
      }
      return filename;
    };
    const normalizeTest = <
      MessageIds extends string,
      Options extends readonly unknown[],
      T extends InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
    >(
      test: T,
    ): T => {
      const { languageOptions = {} } = test;
      if (languageOptions.parser === parser) {
        throw new Error(DUPLICATE_PARSER_ERROR_MESSAGE);
      }
      return {
        ...test,
        filename: getFilename(test.filename, languageOptions.parserOptions),
        languageOptions: {
          ...languageOptions,
          parserOptions: {
            // Re-running simulates --fix mode, which implies an isolated program
            // (i.e. parseAndGenerateServicesCalls[test.filename] > 1).
            disallowAutomaticSingleRunInference: true,
            ...languageOptions.parserOptions,
          },
        },
      };
    };

    const normalizedTests = {
      invalid: rawTests.invalid.map(normalizeTest),
      valid: rawTests.valid
        .map(test => {
          if (typeof test === 'string') {
            return { code: test };
          }
          return test;
        })
        .map(normalizeTest),
    };

    // convenience iterator to make it easy to loop all tests without a concat
    const allTestsIterator = {
      *[Symbol.iterator](): Generator<ValidTestCase<Options>, void> {
        for (const testCase of normalizedTests.valid) {
          yield testCase;
        }
        for (const testCase of normalizedTests.invalid) {
          yield testCase;
        }
      },
    };

    const hasOnly = ((): boolean => {
      for (const test of allTestsIterator) {
        if (test.only) {
          return true;
        }
      }
      return false;
    })();
    if (hasOnly) {
      // if there is an `only: true` - don't try apply constraints - assume that
      // we are in "local development" mode rather than "CI validation" mode
      return normalizedTests;
    }

    const hasConstraints = ((): boolean => {
      for (const test of allTestsIterator) {
        if (
          test.dependencyConstraints &&
          Object.keys(test.dependencyConstraints).length > 0
        ) {
          return true;
        }
      }
      return false;
    })();
    if (!hasConstraints) {
      return normalizedTests;
    }

    /*
    Mark all unsatisfactory tests as `skip: true`.
    We do this instead of just omitting the tests entirely because it gives the
    test framework the opportunity to log the test as skipped rather than the test
    just disappearing without a trace.
    */
    const maybeMarkAsOnly = <
      T extends InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
    >(
      test: T,
    ): T => {
      return {
        ...test,
        skip: !satisfiesAllDependencyConstraints(test.dependencyConstraints),
      };
    };
    normalizedTests.valid = normalizedTests.valid.map(maybeMarkAsOnly);
    normalizedTests.invalid = normalizedTests.invalid.map(maybeMarkAsOnly);

    return normalizedTests;
  }
```
</details>

##### `defineRule(name: string, rule: AnyRuleModule): void`

<details><summary>Code</summary>

```ts
defineRule(name: string, rule: AnyRuleModule): void {
    this.#rules[name] = {
      ...rule,
      // Create a wrapper rule that freezes the `context` properties.
      create(context): RuleListener {
        freezeDeeply(context.options);
        freezeDeeply(context.settings);
        freezeDeeply(context.parserOptions);

        return (typeof rule === 'function' ? rule : rule.create)(context);
      },
    };
  }
```
</details>

##### `#runHook(item: InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>, prop: keyof Pick<typeof item, 'after' | 'before'>): void`

<details><summary>Code</summary>

```ts
#runHook<MessageIds extends string, Options extends readonly unknown[]>(
    item: InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
    prop: keyof Pick<typeof item, 'after' | 'before'>,
  ): void {
    if (hasOwnProperty(item, prop)) {
      assert.strictEqual(
        typeof item[prop],
        'function',
        `Optional test case property '${prop}' must be a function`,
      );
      item[prop]();
    }
  }
```
</details>

##### `run(ruleName: string, rule: RuleModule<MessageIds, Options>, test: RunTests<TSUtils.NoInfer<MessageIds>, TSUtils.NoInfer<Options>>): void`

<details><summary>Code</summary>

```ts
run<MessageIds extends string, Options extends readonly unknown[]>(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    test: RunTests<TSUtils.NoInfer<MessageIds>, TSUtils.NoInfer<Options>>,
  ): void {
    const constructor = this.constructor as typeof RuleTester;

    if (
      this.#testerConfig.dependencyConstraints &&
      !satisfiesAllDependencyConstraints(
        this.#testerConfig.dependencyConstraints,
      )
    ) {
      // for frameworks like mocha or jest that have a "skip" version of their function
      // we can provide a nice skipped test!
      constructor.describeSkip(ruleName, () => {
        constructor.it(
          'All tests skipped due to unsatisfied constructor dependency constraints',
          () => {
            // some frameworks error if there are no assertions
            assert.equal(true, true);
          },
        );
      });

      // don't run any tests because we don't match the base constraint
      return;
    }

    if (!test || typeof test !== 'object') {
      throw new TypeError(
        `Test Scenarios for rule ${ruleName} : Could not find test scenario object`,
      );
    }

    const scenarioErrors: string[] = [];
    REQUIRED_SCENARIOS.forEach(scenarioType => {
      if (!test[scenarioType]) {
        scenarioErrors.push(
          `Could not find any ${scenarioType} test scenarios`,
        );
      }
    });

    if (scenarioErrors.length > 0) {
      throw new Error(
        [
          `Test Scenarios for rule ${ruleName} is invalid:`,
          ...scenarioErrors,
        ].join('\n'),
      );
    }

    const seenValidTestCases = new Set<string>();
    const seenInvalidTestCases = new Set<string>();
    const normalizedTests = this.#normalizeTests(test);

    function getTestMethod(
      test: ValidTestCase<TSUtils.NoInfer<Options>>,
    ): 'it' | 'itOnly' | 'itSkip' {
      if (test.skip) {
        return 'itSkip';
      }
      if (test.only) {
        return 'itOnly';
      }
      return 'it';
    }

    /*
     * This creates a test suite and pipes all supplied info through
     * one of the templates above.
     */
    constructor.describe(ruleName, () => {
      if (normalizedTests.valid.length) {
        constructor.describe('valid', () => {
          normalizedTests.valid.forEach(valid => {
            const testName = ((): string => {
              if (valid.name == null || valid.name.length === 0) {
                return valid.code;
              }
              return valid.name;
            })();
            constructor[getTestMethod(valid)](sanitize(testName), () => {
              try {
                this.#runHook(valid, 'before');
                this.#testValidTemplate(
                  ruleName,
                  rule,
                  valid,
                  seenValidTestCases,
                );
              } finally {
                this.#runHook(valid, 'after');
              }
            });
          });
        });
      }

      if (normalizedTests.invalid.length) {
        constructor.describe('invalid', () => {
          normalizedTests.invalid.forEach(invalid => {
            const name = ((): string => {
              if (invalid.name == null || invalid.name.length === 0) {
                return invalid.code;
              }
              return invalid.name;
            })();
            constructor[getTestMethod(invalid)](sanitize(name), () => {
              try {
                this.#runHook(invalid, 'before');
                this.#testInvalidTemplate(
                  ruleName,
                  rule,
                  // no need to pass no infer type parameter down to private methods
                  invalid as InvalidTestCase<MessageIds, Options>,
                  seenInvalidTestCases,
                );
              } finally {
                this.#runHook(invalid, 'after');
              }
            });
          });
        });
      }
    });
  }
```
</details>

##### `runRuleForItem(ruleName: string, rule: RuleModule<MessageIds, Options>, item: InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>): {
    afterAST: TSESTree.Program;
    beforeAST: TSESTree.Program;
    config: RuleTesterConfig;
    filename?: string;
    messages: Linter.LintMessage[];
    outputs: string[];
  }`

<details><summary>Code</summary>

```ts
private runRuleForItem<
    MessageIds extends string,
    Options extends readonly unknown[],
  >(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    item: InvalidTestCase<MessageIds, Options> | ValidTestCase<Options>,
  ): {
    afterAST: TSESTree.Program;
    beforeAST: TSESTree.Program;
    config: RuleTesterConfig;
    filename?: string;
    messages: Linter.LintMessage[];
    outputs: string[];
  } {
    this.defineRule(ruleName, rule);

    let config: TesterConfigWithDefaults = merge({}, this.#testerConfig, {
      files: ['**'],
      plugins: {
        [RULE_TESTER_PLUGIN]: {
          rules: {
            /**
             * Setup AST getters.
             * The goal is to check whether or not AST was modified when
             * running the rule under test.
             */
            'validate-ast': {
              create(): RuleListener {
                return {
                  Program(node: TSESTree.Program): void {
                    beforeAST = cloneDeeplyExcludesParent(node);
                  },
                  'Program:exit'(node: TSESTree.Program): void {
                    afterAST = node;
                  },
                };
              },
            },
            ...this.#rules,
          },
        },
      },
    });

    // Unlike other properties, we don't want to spread props between different parsers.
    config.languageOptions.parser =
      item.languageOptions?.parser ?? this.#testerConfig.languageOptions.parser;

    let code;
    let filename;
    let beforeAST: TSESTree.Program;
    let afterAST: TSESTree.Program;

    if (typeof item === 'string') {
      code = item;
    } else {
      code = item.code;

      /*
       * Assumes everything on the item is a config except for the
       * parameters used by this tester
       */
      const itemConfig: Record<string, unknown> = { ...item };

      for (const parameter of RULE_TESTER_PARAMETERS) {
        // eslint-disable-next-line @typescript-eslint/no-dynamic-delete
        delete itemConfig[parameter];
      }

      /*
       * Create the config object from the tester config and this item
       * specific configurations.
       */
      config = merge(config, itemConfig);
    }

    if (hasOwnProperty(item, 'only')) {
      assert.ok(
        typeof item.only === 'boolean',
        "Optional test case property 'only' must be a boolean",
      );
    }
    if (hasOwnProperty(item, 'filename')) {
      assert.ok(
        typeof item.filename === 'string',
        "Optional test case property 'filename' must be a string",
      );
      filename = item.filename;
    }

    const prefixedRuleName = `${RULE_TESTER_PLUGIN_PREFIX}${ruleName}`;

    if (hasOwnProperty(item, 'options')) {
      assert(Array.isArray(item.options), 'options must be an array');
      config.rules[prefixedRuleName] = ['error', ...item.options];
    } else {
      config.rules[prefixedRuleName] = 'error';
    }

    config.languageOptions ??= {};
    config.languageOptions.parser ??= defaultParser;
    config.languageOptions.parser = wrapParser(config.languageOptions.parser);

    const schema = getRuleOptionsSchema(rule);

    if (schema) {
      ajv.validateSchema(schema);

      if (ajv.errors) {
        const errors = ajv.errors
          .map(error => {
            const field =
              error.dataPath[0] === '.'
                ? error.dataPath.slice(1)
                : error.dataPath;

            return `\t${field}: ${error.message}`;
          })
          .join('\n');

        throw new Error(
          [`Schema for rule ${ruleName} is invalid:`, errors].join(
            // no space after comma to match eslint core
            ',',
          ),
        );
      }

      /*
       * `ajv.validateSchema` checks for errors in the structure of the schema (by comparing the schema against a "meta-schema"),
       * and it reports those errors individually. However, there are other types of schema errors that only occur when compiling
       * the schema (e.g. using invalid defaults in a schema), and only one of these errors can be reported at a time. As a result,
       * the schema is compiled here separately from checking for `validateSchema` errors.
       */
      try {
        ajv.compile(schema);
      } catch (err) {
        throw new Error(
          `Schema for rule ${ruleName} is invalid: ${(err as Error).message}`,
        );
      }
    }

    validate(config, RULE_TESTER_PLUGIN, id => (id === ruleName ? rule : null));

    // Verify the code.
    let initialMessages: Linter.LintMessage[] | null = null;
    let messages: Linter.LintMessage[] | null = null;
    let fixedResult: SourceCodeFixer.AppliedFixes | null = null;
    let passNumber = 0;
    const outputs: string[] = [];
    const configWithoutCustomKeys = omitCustomConfigProperties(config);
    const linter = this.#getLinterForFilename(filename);

    do {
      passNumber++;

      const SourceCodePrototype = SourceCode.prototype as Record<
        ForbiddenMethodName,
        ForbiddenFunction
      >;

      const { applyInlineConfig, applyLanguageOptions, finalize } =
        SourceCodePrototype;

      try {
        forbiddenMethods.forEach(methodName => {
          SourceCodePrototype[methodName] = throwForbiddenMethodError(
            methodName,
            SourceCodePrototype,
          );
        });

        const actualConfig = merge(configWithoutCustomKeys, {
          languageOptions: {
            ...configWithoutCustomKeys.languageOptions,
            parserOptions: {
              ecmaVersion: 'latest',
              sourceType: 'module',
              ...configWithoutCustomKeys.languageOptions?.parserOptions,
            },
          },
          linterOptions: {
            reportUnusedDisableDirectives: 1,
            ...configWithoutCustomKeys.linterOptions,
          },
        });
        messages = linter.verify(code, actualConfig, filename);
      } finally {
        SourceCodePrototype.applyInlineConfig = applyInlineConfig;
        SourceCodePrototype.applyLanguageOptions = applyLanguageOptions;
        SourceCodePrototype.finalize = finalize;
      }

      initialMessages ??= messages;

      if (messages.length === 0) {
        break;
      }

      const fatalErrorMessage = messages.find(m => m.fatal);
      assert(
        !fatalErrorMessage,
        `A fatal parsing error occurred: ${fatalErrorMessage?.message}`,
      );

      fixedResult = SourceCodeFixer.applyFixes(code, messages);
      if (fixedResult.output === code) {
        break;
      }
      code = fixedResult.output;
      outputs.push(code);

      // Verify if autofix makes a syntax error or not.
      const errorMessageInFix = linter
        .verify(fixedResult.output, configWithoutCustomKeys, filename)
        .find(m => m.fatal);

      assert(
        !errorMessageInFix,
        [
          'A fatal parsing error occurred in autofix.',
          `Error: ${errorMessageInFix?.message}`,
          'Autofix output:',
          fixedResult.output,
        ].join('\n'),
      );
    } while (fixedResult.fixed && passNumber < 10);

    return {
      config,
      filename,
      messages: initialMessages,
      outputs,
      // is definitely assigned within the `@rule-tester/validate-ast` rule
      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      beforeAST: beforeAST!,
      // is definitely assigned within the `@rule-tester/validate-ast` rule
      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      afterAST: cloneDeeplyExcludesParent(afterAST!),
    };
  }
```
</details>

##### `#testValidTemplate(ruleName: string, rule: RuleModule<MessageIds, Options>, itemIn: string | ValidTestCase<Options>, seenValidTestCases: Set<string>): void`

<details><summary>Code</summary>

```ts
#testValidTemplate<
    MessageIds extends string,
    Options extends readonly unknown[],
  >(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    itemIn: string | ValidTestCase<Options>,
    seenValidTestCases: Set<string>,
  ): void {
    const item: ValidTestCase<Options> =
      typeof itemIn === 'object' ? itemIn : { code: itemIn };

    assert.ok(
      typeof item.code === 'string',
      "Test case must specify a string value for 'code'",
    );
    if (item.name) {
      assert.ok(
        typeof item.name === 'string',
        "Optional test case property 'name' must be a string",
      );
    }

    checkDuplicateTestCase(item, seenValidTestCases);

    const result = this.runRuleForItem(ruleName, rule, item);
    const messages = result.messages;

    assert.strictEqual(
      messages.length,
      0,
      util.format(
        'Should have no errors but had %d: %s',
        messages.length,
        util.inspect(messages),
      ),
    );

    assertASTDidntChange(result.beforeAST, result.afterAST);
  }
```
</details>

##### `#testInvalidTemplate(ruleName: string, rule: RuleModule<MessageIds, Options>, item: InvalidTestCase<MessageIds, Options>, seenInvalidTestCases: Set<string>): void`

<details><summary>Code</summary>

```ts
#testInvalidTemplate<
    MessageIds extends string,
    Options extends readonly unknown[],
  >(
    ruleName: string,
    rule: RuleModule<MessageIds, Options>,
    item: InvalidTestCase<MessageIds, Options>,
    seenInvalidTestCases: Set<string>,
  ): void {
    assert.ok(
      typeof item.code === 'string',
      "Test case must specify a string value for 'code'",
    );
    if (item.name) {
      assert.ok(
        typeof item.name === 'string',
        "Optional test case property 'name' must be a string",
      );
    }
    assert.ok(
      item.errors || item.errors === 0,
      `Did not specify errors for an invalid test of ${ruleName}`,
    );

    if (Array.isArray(item.errors) && item.errors.length === 0) {
      assert.fail('Invalid cases must have at least one error');
    }

    checkDuplicateTestCase(item, seenInvalidTestCases);

    const ruleHasMetaMessages =
      hasOwnProperty(rule, 'meta') && hasOwnProperty(rule.meta, 'messages');
    const friendlyIDList = ruleHasMetaMessages
      ? `[${Object.keys(rule.meta.messages)
          .map(key => `'${key}'`)
          .join(', ')}]`
      : null;

    const result = this.runRuleForItem(ruleName, rule, item);
    const messages = result.messages.map(message => ({
      ...message,
      ...(message.ruleId && {
        ruleId: message.ruleId.startsWith(RULE_TESTER_PLUGIN_PREFIX)
          ? message.ruleId.slice(RULE_TESTER_PLUGIN_PREFIX.length)
          : message.ruleId,
      }),
    }));

    for (const message of messages) {
      if (hasOwnProperty(message, 'suggestions')) {
        const seenMessageIndices = new Map<string, number>();

        for (let i = 0; i < message.suggestions.length; i += 1) {
          const suggestionMessage = message.suggestions[i].desc;
          const previous = seenMessageIndices.get(suggestionMessage);

          assert.ok(
            !seenMessageIndices.has(suggestionMessage),
            `Suggestion message '${suggestionMessage}' reported from suggestion ${i} was previously reported by suggestion ${previous}. Suggestion messages should be unique within an error.`,
          );
          seenMessageIndices.set(suggestionMessage, i);
        }
      }
    }

    if (typeof item.errors === 'number') {
      if (item.errors === 0) {
        assert.fail("Invalid cases must have 'error' value greater than 0");
      }

      assert.strictEqual(
        messages.length,
        item.errors,
        util.format(
          'Should have %d error%s but had %d: %s',
          item.errors,
          item.errors === 1 ? '' : 's',
          messages.length,
          util.inspect(messages),
        ),
      );
    } else {
      assert.strictEqual(
        messages.length,
        item.errors.length,
        util.format(
          'Should have %d error%s but had %d: %s',
          item.errors.length,
          item.errors.length === 1 ? '' : 's',
          messages.length,
          util.inspect(messages),
        ),
      );

      const hasMessageOfThisRule = messages.some(m => m.ruleId === ruleName);

      // console.log({ messages });
      for (let i = 0, l = item.errors.length; i < l; i++) {
        const error = item.errors[i];
        const message = messages[i];

        assert(
          hasMessageOfThisRule,
          'Error rule name should be the same as the name of the rule being tested',
        );

        if (typeof error === 'string' || error instanceof RegExp) {
          // Just an error message.
          assertMessageMatches(message.message, error);
          assert.ok(
            message.suggestions == null,
            `Error at index ${i} has suggestions. Please convert the test error into an object and specify 'suggestions' property on it to test suggestions.`,
          );
        } else if (typeof error === 'object' && error != null) {
          /*
           * Error object.
           * This may have a message, messageId, data, node type, line, and/or
           * column.
           */

          Object.keys(error).forEach(propertyName => {
            assert.ok(
              ERROR_OBJECT_PARAMETERS.has(propertyName),
              `Invalid error property name '${propertyName}'. Expected one of ${FRIENDLY_ERROR_OBJECT_PARAMETER_LIST}.`,
            );
          });

          // @ts-expect-error -- we purposely don't define `message` on our types as the current standard is `messageId`
          if (hasOwnProperty(error, 'message')) {
            assert.ok(
              !hasOwnProperty(error, 'messageId'),
              "Error should not specify both 'message' and a 'messageId'.",
            );
            assert.ok(
              !hasOwnProperty(error, 'data'),
              "Error should not specify both 'data' and 'message'.",
            );
            assertMessageMatches(
              message.message,
              // @ts-expect-error -- we purposely don't define `message` on our types as the current standard is `messageId`
              error.message as unknown,
            );
          } else if (hasOwnProperty(error, 'messageId')) {
            assert.ok(
              ruleHasMetaMessages,
              "Error can not use 'messageId' if rule under test doesn't define 'meta.messages'.",
            );
            if (!hasOwnProperty(rule.meta.messages, error.messageId)) {
              assert(
                false,
                `Invalid messageId '${error.messageId}'. Expected one of ${friendlyIDList}.`,
              );
            }
            assert.strictEqual(
              message.messageId,
              error.messageId,
              `messageId '${message.messageId}' does not match expected messageId '${error.messageId}'.`,
            );

            const unsubstitutedPlaceholders =
              getUnsubstitutedMessagePlaceholders(
                message.message,
                rule.meta.messages[message.messageId],
                error.data,
              );

            assert.ok(
              unsubstitutedPlaceholders.length === 0,
              `The reported message has ${unsubstitutedPlaceholders.length > 1 ? `unsubstituted placeholders: ${unsubstitutedPlaceholders.map(name => `'${name}'`).join(', ')}` : `an unsubstituted placeholder '${unsubstitutedPlaceholders[0]}'`}. Please provide the missing ${unsubstitutedPlaceholders.length > 1 ? 'values' : 'value'} via the 'data' property in the context.report() call.`,
            );

            if (hasOwnProperty(error, 'data')) {
              /*
               *  if data was provided, then directly compare the returned message to a synthetic
               *  interpolated message using the same message ID and data provided in the test.
               *  See https://github.com/eslint/eslint/issues/9890 for context.
               */
              const unformattedOriginalMessage =
                rule.meta.messages[error.messageId];
              const rehydratedMessage = interpolate(
                unformattedOriginalMessage,
                error.data,
              );

              assert.strictEqual(
                message.message,
                rehydratedMessage,
                `Hydrated message "${rehydratedMessage}" does not match "${message.message}"`,
              );
            }
          } else {
            assert.fail(
              "Test error must specify either a 'messageId' or 'message'.",
            );
          }

          if (error.type) {
            assert.strictEqual(
              message.nodeType,
              error.type,
              `Error type should be ${error.type}, found ${message.nodeType}`,
            );
          }

          if (hasOwnProperty(error, 'line')) {
            assert.strictEqual(
              message.line,
              error.line,
              `Error line should be ${error.line}`,
            );
          }

          if (hasOwnProperty(error, 'column')) {
            assert.strictEqual(
              message.column,
              error.column,
              `Error column should be ${error.column}`,
            );
          }

          if (hasOwnProperty(error, 'endLine')) {
            assert.strictEqual(
              message.endLine,
              error.endLine,
              `Error endLine should be ${error.endLine}`,
            );
          }

          if (hasOwnProperty(error, 'endColumn')) {
            assert.strictEqual(
              message.endColumn,
              error.endColumn,
              `Error endColumn should be ${error.endColumn}`,
            );
          }

          assert.ok(
            !message.suggestions || hasOwnProperty(error, 'suggestions'),
            `Error at index ${i} has suggestions. Please specify 'suggestions' property on the test error object.`,
          );
          if (hasOwnProperty(error, 'suggestions')) {
            // Support asserting there are no suggestions
            const expectsSuggestions = Array.isArray(error.suggestions)
              ? error.suggestions.length > 0
              : Boolean(error.suggestions);
            const hasSuggestions = message.suggestions != null;
            // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
            const messageSuggestions = message.suggestions!;

            if (!hasSuggestions && expectsSuggestions) {
              assert.ok(
                !error.suggestions,
                `Error should have suggestions on error with message: "${message.message}"`,
              );
            } else if (hasSuggestions) {
              assert.ok(
                expectsSuggestions,
                `Error should have no suggestions on error with message: "${message.message}"`,
              );
              if (typeof error.suggestions === 'number') {
                assert.strictEqual(
                  messageSuggestions.length,
                  error.suggestions,
                  // It is possible that error.suggestions is a number
                  // eslint-disable-next-line @typescript-eslint/restrict-template-expressions
                  `Error should have ${error.suggestions} suggestions. Instead found ${messageSuggestions.length} suggestions`,
                );
              } else if (Array.isArray(error.suggestions)) {
                assert.strictEqual(
                  messageSuggestions.length,
                  error.suggestions.length,
                  `Error should have ${error.suggestions.length} suggestions. Instead found ${messageSuggestions.length} suggestions`,
                );

                error.suggestions.forEach(
                  (expectedSuggestion: SuggestionOutput<MessageIds>, index) => {
                    assert.ok(
                      typeof expectedSuggestion === 'object' &&
                        expectedSuggestion != null,
                      "Test suggestion in 'suggestions' array must be an object.",
                    );
                    Object.keys(expectedSuggestion).forEach(propertyName => {
                      assert.ok(
                        SUGGESTION_OBJECT_PARAMETERS.has(propertyName),
                        `Invalid suggestion property name '${propertyName}'. Expected one of ${FRIENDLY_SUGGESTION_OBJECT_PARAMETER_LIST}.`,
                      );
                    });

                    const actualSuggestion = messageSuggestions[index];
                    const suggestionPrefix = `Error Suggestion at index ${index}:`;

                    // @ts-expect-error -- we purposely don't define `desc` on our types as the current standard is `messageId`
                    if (hasOwnProperty(expectedSuggestion, 'desc')) {
                      // @ts-expect-error -- we purposely don't define `desc` on our types as the current standard is `messageId`
                      const expectedDesc = expectedSuggestion.desc as string;

                      assert.ok(
                        !hasOwnProperty(expectedSuggestion, 'data'),
                        `${suggestionPrefix} Test should not specify both 'desc' and 'data'.`,
                      );
                      assert.ok(
                        !hasOwnProperty(expectedSuggestion, 'messageId'),
                        `${suggestionPrefix} Test should not specify both 'desc' and 'messageId'.`,
                      );
                      assert.strictEqual(
                        actualSuggestion.desc,
                        expectedDesc,
                        `${suggestionPrefix} desc should be "${expectedDesc}" but got "${actualSuggestion.desc}" instead.`,
                      );
                    } else if (
                      hasOwnProperty(expectedSuggestion, 'messageId')
                    ) {
                      assert.ok(
                        ruleHasMetaMessages,
                        `${suggestionPrefix} Test can not use 'messageId' if rule under test doesn't define 'meta.messages'.`,
                      );
                      assert.ok(
                        hasOwnProperty(
                          rule.meta.messages,
                          expectedSuggestion.messageId,
                        ),
                        `${suggestionPrefix} Test has invalid messageId '${expectedSuggestion.messageId}', the rule under test allows only one of ${friendlyIDList}.`,
                      );
                      assert.strictEqual(
                        actualSuggestion.messageId,
                        expectedSuggestion.messageId,
                        `${suggestionPrefix} messageId should be '${expectedSuggestion.messageId}' but got '${actualSuggestion.messageId}' instead.`,
                      );

                      const unsubstitutedPlaceholders =
                        getUnsubstitutedMessagePlaceholders(
                          actualSuggestion.desc,
                          rule.meta.messages[expectedSuggestion.messageId],
                          expectedSuggestion.data,
                        );

                      assert.ok(
                        unsubstitutedPlaceholders.length === 0,
                        `The message of the suggestion has ${unsubstitutedPlaceholders.length > 1 ? `unsubstituted placeholders: ${unsubstitutedPlaceholders.map(name => `'${name}'`).join(', ')}` : `an unsubstituted placeholder '${unsubstitutedPlaceholders[0]}'`}. Please provide the missing ${unsubstitutedPlaceholders.length > 1 ? 'values' : 'value'} via the 'data' property for the suggestion in the context.report() call.`,
                      );

                      if (hasOwnProperty(expectedSuggestion, 'data')) {
                        const unformattedMetaMessage =
                          rule.meta.messages[expectedSuggestion.messageId];
                        const rehydratedDesc = interpolate(
                          unformattedMetaMessage,
                          expectedSuggestion.data,
                        );

                        assert.strictEqual(
                          actualSuggestion.desc,
                          rehydratedDesc,
                          `${suggestionPrefix} Hydrated test desc "${rehydratedDesc}" does not match received desc "${actualSuggestion.desc}".`,
                        );
                      }
                    } else if (hasOwnProperty(expectedSuggestion, 'data')) {
                      assert.fail(
                        `${suggestionPrefix} Test must specify 'messageId' if 'data' is used.`,
                      );
                    } else {
                      assert.fail(
                        `${suggestionPrefix} Test must specify either 'messageId' or 'desc'.`,
                      );
                    }

                    assert.ok(
                      hasOwnProperty(expectedSuggestion, 'output'),
                      `${suggestionPrefix} The "output" property is required.`,
                    );
                    const codeWithAppliedSuggestion =
                      SourceCodeFixer.applyFixes(item.code, [
                        actualSuggestion,
                      ]).output;

                    // Verify if suggestion fix makes a syntax error or not.
                    const errorMessageInSuggestion = this.#getLinterForFilename(
                      item.filename,
                    )
                      .verify(
                        codeWithAppliedSuggestion,
                        omitCustomConfigProperties(result.config),
                        result.filename,
                      )
                      .find(m => m.fatal);

                    assert(
                      !errorMessageInSuggestion,
                      [
                        'A fatal parsing error occurred in suggestion fix.',
                        `Error: ${errorMessageInSuggestion?.message}`,
                        'Suggestion output:',
                        codeWithAppliedSuggestion,
                      ].join('\n'),
                    );

                    assert.strictEqual(
                      codeWithAppliedSuggestion,
                      expectedSuggestion.output,
                      `Expected the applied suggestion fix to match the test suggestion output for suggestion at index: ${index} on error with message: "${message.message}"`,
                    );
                    assert.notStrictEqual(
                      expectedSuggestion.output,
                      item.code,
                      `The output of a suggestion should differ from the original source code for suggestion at index: ${index} on error with message: "${message.message}"`,
                    );
                  },
                );
              } else {
                assert.fail(
                  "Test error object property 'suggestions' should be an array or a number",
                );
              }
            }
          }
        } else {
          // Message was an unexpected type
          assert.fail(
            `Error should be a string, object, or RegExp, but found (${util.inspect(
              message,
            )})`,
          );
        }
      }
    }

    if (hasOwnProperty(item, 'output')) {
      if (item.output == null) {
        if (result.outputs.length) {
          assert.strictEqual(
            result.outputs[0],
            item.code,
            'Expected no autofixes to be suggested.',
          );
        }
      } else if (typeof item.output === 'string') {
        assert(result.outputs.length > 0, 'Expected autofix to be suggested.');
        assert.strictEqual(
          result.outputs[0],
          item.output,
          'Output is incorrect.',
        );
        if (result.outputs.length) {
          assert.deepStrictEqual(
            result.outputs,
            [item.output],
            'Multiple autofixes are required due to overlapping fix ranges - please use the array form of output to declare all of the expected autofix passes.',
          );
        }
      } else {
        assert(result.outputs.length > 0, 'Expected autofix to be suggested.');
        assert.deepStrictEqual(
          result.outputs,
          item.output,
          'Outputs do not match.',
        );
      }
    } else if (result.outputs.length) {
      assert.strictEqual(
        result.outputs[0],
        item.code,
        "The rule fixed the code. Please add 'output' property.",
      );
    }

    assertASTDidntChange(result.beforeAST, result.afterAST);
  }
```
</details>


---

## Type Aliases

### `ForbiddenFunction`

```ts
type ForbiddenFunction = (this: WeakKey, ...args: never[]) => unknown;
```

### `ForbiddenMethodName`

```ts
type ForbiddenMethodName = (typeof forbiddenMethods)[number];
```


---