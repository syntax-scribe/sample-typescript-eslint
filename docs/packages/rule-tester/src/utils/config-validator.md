[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `config-validator.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 7
- **Classes**: 0
- **Imports**: 13
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/config-validator.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AnyRuleModule` | `@typescript-eslint/utils/ts-eslint` |
| `Linter` | `@typescript-eslint/utils/ts-eslint` |
| `AdditionalPropertiesParams` | `ajv` |
| `AjvErrorObject` | `ajv` |
| `ValidateFunction` | `ajv` |
| `builtinRules` | `eslint/use-at-your-own-risk` |
| `util` | `node:util` |
| `TesterConfigWithDefaults` | `../types` |
| `ajvBuilder` | `./ajv` |
| `emitDeprecationWarning` | `./deprecation-warnings` |
| `flatConfigSchema` | `./flat-config-schema` |
| `getRuleOptionsSchema` | `./getRuleOptionsSchema` |
| `hasOwnProperty` | `./hasOwnProperty` |


---

## Functions

### `validateRuleSeverity(options: Linter.RuleEntry): number | string`

<details><summary>Code</summary>

```ts
function validateRuleSeverity(options: Linter.RuleEntry): number | string {
  const severity = Array.isArray(options) ? options[0] : options;
  const normSeverity =
    typeof severity === 'string'
      ? (severityMap[severity.toLowerCase() as Linter.SeverityString] as
          | number
          | undefined)
      : (severity as number);

  if (normSeverity === 0 || normSeverity === 1 || normSeverity === 2) {
    return normSeverity;
  }

  throw new Error(
    `\tSeverity should be one of the following: 0 = off, 1 = warn, 2 = error (you passed '${util
      .inspect(severity)
      .replaceAll("'", '"')
      .replaceAll('\n', '')}').\n`,
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Validates a rule's severity and returns the severity value. Throws an error if the severity is invalid.
 * @param options The given options for the rule.
 * @throws {Error} Wrong severity value.
 */
```

- **Parameters**:
  - `options: Linter.RuleEntry`
- **Return Type**: `number | string`
- **Calls**:
  - `Array.isArray`
  - `severity.toLowerCase`
  - `util
      .inspect(severity)
      .replaceAll("'", '"')
      .replaceAll`
### `validateRuleSchema(rule: AnyRuleModule, localOptions: unknown[]): void`

<details><summary>Code</summary>

```ts
function validateRuleSchema(
  rule: AnyRuleModule,
  localOptions: unknown[],
): void {
  if (!ruleValidators.has(rule)) {
    const schema = getRuleOptionsSchema(rule);

    if (schema) {
      ruleValidators.set(rule, ajv.compile(schema));
    }
  }

  const validateRule = ruleValidators.get(rule);

  if (validateRule) {
    void validateRule(localOptions);
    if (validateRule.errors) {
      throw new Error(
        validateRule.errors
          .map(
            error =>
              `\tValue ${JSON.stringify(error.data)} ${error.message}.\n`,
          )
          .join(''),
      );
    }
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Validates the non-severity options passed to a rule, based on its schema.
 * @param rule The rule to validate
 * @param localOptions The options for the rule, excluding severity
 * @throws {Error} Any rule validation errors.
 */
```

- **Parameters**:
  - `rule: AnyRuleModule`
  - `localOptions: unknown[]`
- **Return Type**: `void`
- **Calls**:
  - `ruleValidators.has`
  - `getRuleOptionsSchema (from ./getRuleOptionsSchema)`
  - `ruleValidators.set`
  - `ajv.compile`
  - `ruleValidators.get`
  - `validateRule`
  - `validateRule.errors
          .map(
            error =>
              `\tValue ${JSON.stringify(error.data)} ${error.message}.\n`,
          )
          .join`
### `validateRuleOptions(rule: AnyRuleModule, ruleId: string, options: Linter.RuleEntry, source: string | null): void`

<details><summary>Code</summary>

```ts
function validateRuleOptions(
  rule: AnyRuleModule,
  ruleId: string,
  options: Linter.RuleEntry,
  source: string | null = null,
): void {
  try {
    const severity = validateRuleSeverity(options);

    if (severity !== 0) {
      validateRuleSchema(rule, Array.isArray(options) ? options.slice(1) : []);
    }
  } catch (err) {
    const enhancedMessage = `Configuration for rule "${ruleId}" is invalid:\n${
      (err as Error).message
    }`;

    if (typeof source === 'string') {
      throw new Error(`${source}:\n\t${enhancedMessage}`);
    } else {
      throw new Error(enhancedMessage);
    }
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Validates a rule's options against its schema.
 * @param rule The rule that the config is being validated for
 * @param ruleId The rule's unique name.
 * @param options The given options for the rule.
 * @param source The name of the configuration source to report in any errors. If null or undefined,
 * no source is prepended to the message.
 * @throws {Error} Upon any bad rule configuration.
 */
```

- **Parameters**:
  - `rule: AnyRuleModule`
  - `ruleId: string`
  - `options: Linter.RuleEntry`
  - `source: string | null`
- **Return Type**: `void`
- **Calls**:
  - `validateRuleSeverity`
  - `validateRuleSchema`
  - `Array.isArray`
  - `options.slice`
### `validateRules(rulesConfig: Linter.RulesRecord | undefined, source: string, getAdditionalRule: GetAdditionalRule): void`

<details><summary>Code</summary>

```ts
function validateRules(
  rulesConfig: Linter.RulesRecord | undefined,
  source: string,
  getAdditionalRule: GetAdditionalRule,
): void {
  if (!rulesConfig) {
    return;
  }

  Object.keys(rulesConfig).forEach(id => {
    const rule = getAdditionalRule(id) ?? builtinRules.get(id) ?? null;
    if (rule == null) {
      return;
    }

    // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
    validateRuleOptions(rule, id, rulesConfig[id]!, source);
  });
}
```
</details>

- **JSDoc**:
```ts
/**
 * Validates a rules config object
 * @param rulesConfig The rules config object to validate.
 * @param source The name of the configuration source to report in any errors.
 * @param getAdditionalRule A map from strings to loaded rules
 */
```

- **Parameters**:
  - `rulesConfig: Linter.RulesRecord | undefined`
  - `source: string`
  - `getAdditionalRule: GetAdditionalRule`
- **Return Type**: `void`
- **Calls**:
  - `Object.keys(rulesConfig).forEach`
  - `getAdditionalRule`
  - `builtinRules.get`
  - `validateRuleOptions`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x3)
```

### `formatErrors(errors: AjvErrorObject[]): string`

<details><summary>Code</summary>

```ts
function formatErrors(errors: AjvErrorObject[]): string {
  return errors
    .map(error => {
      if (error.keyword === 'additionalProperties') {
        const params = error.params as AdditionalPropertiesParams;
        const formattedPropertyPath = error.dataPath.length
          ? `${error.dataPath.slice(1)}.${params.additionalProperty}`
          : params.additionalProperty;

        return `Unexpected top-level property "${formattedPropertyPath}"`;
      }
      if (error.keyword === 'type') {
        const formattedField = error.dataPath.slice(1);
        // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
        const formattedExpectedType = Array.isArray(error.schema)
          ? error.schema.join('/')
          : error.schema;
        const formattedValue = JSON.stringify(error.data);

        return `Property "${formattedField}" is the wrong type (expected ${formattedExpectedType} but got \`${formattedValue}\`)`;
      }

      const field =
        error.dataPath[0] === '.' ? error.dataPath.slice(1) : error.dataPath;

      return `"${field}" ${error.message}. Value: ${JSON.stringify(
        error.data,
      )}`;
    })
    .map(message => `\t- ${message}.\n`)
    .join('');
}
```
</details>

- **JSDoc**:
```ts
/**
 * Formats an array of schema validation errors.
 */
```

- **Parameters**:
  - `errors: AjvErrorObject[]`
- **Return Type**: `string`
- **Calls**:
  - `errors
    .map(error => {
      if (error.keyword === 'additionalProperties') {
        const params = error.params as AdditionalPropertiesParams;
        const formattedPropertyPath = error.dataPath.length
          ? `${error.dataPath.slice(1)}.${params.additionalProperty}`
          : params.additionalProperty;

        return `Unexpected top-level property "${formattedPropertyPath}"`;
      }
      if (error.keyword === 'type') {
        const formattedField = error.dataPath.slice(1);
        // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
        const formattedExpectedType = Array.isArray(error.schema)
          ? error.schema.join('/')
          : error.schema;
        const formattedValue = JSON.stringify(error.data);

        return `Property "${formattedField}" is the wrong type (expected ${formattedExpectedType} but got \`${formattedValue}\`)`;
      }

      const field =
        error.dataPath[0] === '.' ? error.dataPath.slice(1) : error.dataPath;

      return `"${field}" ${error.message}. Value: ${JSON.stringify(
        error.data,
      )}`;
    })
    .map(message => `\t- ${message}.\n`)
    .join`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-unsafe-assignment (x2)
```

### `validateConfigSchema(config: TesterConfigWithDefaults, source: string): void`

<details><summary>Code</summary>

```ts
function validateConfigSchema(
  config: TesterConfigWithDefaults,
  source: string,
): void {
  validateSchema ??= ajv.compile(flatConfigSchema);

  if (!validateSchema(config)) {
    throw new Error(
      `ESLint configuration in ${source} is invalid:\n${formatErrors(
        // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
        validateSchema.errors!,
      )}`,
    );
  }

  // @ts-expect-error -- intentional deprecated check
  if (hasOwnProperty(config, 'ecmaFeatures')) {
    emitDeprecationWarning(source, 'ESLINT_LEGACY_ECMAFEATURES');
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Validates the top level properties of the config object.
 * @param config The config object to validate.
 * @param source The name of the configuration source to report in any errors.
 * @throws {Error} For any config invalid per the schema.
 */
```

- **Parameters**:
  - `config: TesterConfigWithDefaults`
  - `source: string`
- **Return Type**: `void`
- **Calls**:
  - `ajv.compile`
  - `validateSchema`
  - `formatErrors`
  - `hasOwnProperty (from ./hasOwnProperty)`
  - `emitDeprecationWarning (from ./deprecation-warnings)`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x3)
// @ts-expect-error -- intentional deprecated check
```

### `validate(config: TesterConfigWithDefaults, source: string, getAdditionalRule: GetAdditionalRule): void`

<details><summary>Code</summary>

```ts
export function validate(
  config: TesterConfigWithDefaults,
  source: string,
  getAdditionalRule: GetAdditionalRule,
): void {
  validateConfigSchema(config, source);
  validateRules(config.rules, source, getAdditionalRule);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Validates an entire config object.
 * @param config The config object to validate.
 * @param source The name of the configuration source to report in any errors.
 * @param getAdditionalRule A map from strings to loaded rules.
 */
```

- **Parameters**:
  - `config: TesterConfigWithDefaults`
  - `source: string`
  - `getAdditionalRule: GetAdditionalRule`
- **Return Type**: `void`
- **Calls**:
  - `validateConfigSchema`
  - `validateRules`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `GetAdditionalRule`

```ts
type GetAdditionalRule = (ruleId: string) => AnyRuleModule | null;
```


---