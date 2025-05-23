[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `flat-config-schema.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 10
- **Classes**: 4
- **Imports**: 3
- **Interfaces**: 1
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/flat-config-schema.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Processor` | `@typescript-eslint/utils/ts-eslint` |
| `SharedConfig` | `@typescript-eslint/utils/ts-eslint` |
| `normalizeSeverityToNumber` | `./severity` |


---

## Functions

### `isNonNullObject(value: unknown): boolean`

<details><summary>Code</summary>

```ts
function isNonNullObject(value: unknown): boolean {
  // eslint-disable-next-line eqeqeq, @typescript-eslint/internal/eqeq-nullish
  return typeof value === 'object' && value !== null;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if a value is a non-null object.
 * @param value The value to check.
 * @returns `true` if the value is a non-null object.
 */
```

- **Parameters**:
  - `value: unknown`
- **Return Type**: `boolean`
- **Internal Comments**:
```
// eslint-disable-next-line eqeqeq, @typescript-eslint/internal/eqeq-nullish
```

### `isNonArrayObject(value: unknown): boolean`

<details><summary>Code</summary>

```ts
function isNonArrayObject(value: unknown): boolean {
  return isNonNullObject(value) && !Array.isArray(value);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if a value is a non-null non-array object.
 * @param value The value to check.
 * @returns `true` if the value is a non-null non-array object.
 */
```

- **Parameters**:
  - `value: unknown`
- **Return Type**: `boolean`
- **Calls**:
  - `isNonNullObject`
  - `Array.isArray`
### `deepMerge(first: First, second: Second, mergeMap: Map<First | Second, Map<First | Second, First & Second>>): First & Second`

<details><summary>Code</summary>

```ts
function deepMerge<First extends object, Second extends object>(
  first: First,
  second: Second,
  mergeMap = new Map<First | Second, Map<First | Second, First & Second>>(),
): First & Second {
  let secondMergeMap = mergeMap.get(first);

  if (secondMergeMap) {
    const result = secondMergeMap.get(second);

    if (result) {
      // If this combination of first and second arguments has been already visited, return the previously created result.
      return result;
    }
  } else {
    secondMergeMap = new Map();
    mergeMap.set(first, secondMergeMap);
  }

  /*
   * First create a result object where properties from the second object
   * overwrite properties from the first. This sets up a baseline to use
   * later rather than needing to inspect and change every property
   * individually.
   */
  const result = {
    ...first,
    ...second,
  } as First & ObjectLike & Second;

  delete (result as ObjectLike).__proto__; // don't merge own property "__proto__"

  // Store the pending result for this combination of first and second arguments.
  secondMergeMap.set(second, result);

  for (const key of Object.keys(second)) {
    // avoid hairy edge case
    if (
      key === '__proto__' ||
      !Object.prototype.propertyIsEnumerable.call(first, key)
    ) {
      continue;
    }

    const firstValue = (first as ObjectLike)[key] as object | undefined;
    const secondValue = (second as ObjectLike)[key] as object | undefined;

    if (isNonArrayObject(firstValue) && isNonArrayObject(secondValue)) {
      (result as ObjectLike)[key] = deepMerge(
        // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
        firstValue!,
        // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
        secondValue!,
        mergeMap,
      );
      // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
    } else if (secondValue === undefined) {
      (result as ObjectLike)[key] = firstValue;
    }
  }

  return result;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Deeply merges two non-array objects.
 * @param first The base object.
 * @param second The overrides object.
 * @param mergeMap Maps the combination of first and second arguments to a merged result.
 * @returns An object with properties from both first and second.
 */
```

- **Parameters**:
  - `first: First`
  - `second: Second`
  - `mergeMap: Map<First | Second, Map<First | Second, First & Second>>`
- **Return Type**: `First & Second`
- **Calls**:
  - `mergeMap.get`
  - `secondMergeMap.get`
  - `mergeMap.set`
  - `secondMergeMap.set`
  - `Object.keys`
  - `Object.prototype.propertyIsEnumerable.call`
  - `isNonArrayObject`
  - `deepMerge`
- **Internal Comments**:
```
// If this combination of first and second arguments has been already visited, return the previously created result.
/*
   * First create a result object where properties from the second object
   * overwrite properties from the first. This sets up a baseline to use
   * later rather than needing to inspect and change every property
   * individually.
   */ (x2)
// Store the pending result for this combination of first and second arguments. (x4)
// avoid hairy edge case
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x4)
```

### `normalizeRuleOptions(ruleOptions: SharedConfig.RuleLevel | SharedConfig.RuleLevelAndOptions): SharedConfig.RuleLevelAndOptions`

<details><summary>Code</summary>

```ts
function normalizeRuleOptions(
  ruleOptions: SharedConfig.RuleLevel | SharedConfig.RuleLevelAndOptions,
): SharedConfig.RuleLevelAndOptions {
  const finalOptions = Array.isArray(ruleOptions)
    ? [...ruleOptions]
    : [ruleOptions];

  finalOptions[0] = ruleSeverities.get(
    finalOptions[0] as SharedConfig.RuleLevel,
  );

  return structuredClone(finalOptions as SharedConfig.RuleLevelAndOptions);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Normalizes the rule options config for a given rule by ensuring that
 * it is an array and that the first item is 0, 1, or 2.
 * @param ruleOptions The rule options config.
 * @returns An array of rule options.
 */
```

- **Parameters**:
  - `ruleOptions: SharedConfig.RuleLevel | SharedConfig.RuleLevelAndOptions`
- **Return Type**: `SharedConfig.RuleLevelAndOptions`
- **Calls**:
  - `Array.isArray`
  - `ruleSeverities.get`
  - `structuredClone`
### `hasMethod(object: Record<string, unknown>): boolean`

<details><summary>Code</summary>

```ts
function hasMethod(object: Record<string, unknown>): boolean {
  for (const key of Object.keys(object)) {
    if (typeof object[key] === 'function') {
      return true;
    }
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Determines if an object has any methods.
 * @param object The object to check.
 * @returns `true` if the object has any methods.
 */
```

- **Parameters**:
  - `object: Record<string, unknown>`
- **Return Type**: `boolean`
- **Calls**:
  - `Object.keys`
### `assertIsRuleOptions(ruleId: string, value: unknown): void`

<details><summary>Code</summary>

```ts
function assertIsRuleOptions(ruleId: string, value: unknown): void {
  if (
    typeof value !== 'string' &&
    typeof value !== 'number' &&
    !Array.isArray(value)
  ) {
    throw new InvalidRuleOptionsError(ruleId, value);
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Validates that a value is a valid rule options entry.
 * @param ruleId Rule name being configured.
 * @param value The value to check.
 * @throws {InvalidRuleOptionsError} If the value isn't a valid rule options.
 */
```

- **Parameters**:
  - `ruleId: string`
  - `value: unknown`
- **Return Type**: `void`
- **Calls**:
  - `Array.isArray`
### `assertIsRuleSeverity(ruleId: string, value: unknown): void`

<details><summary>Code</summary>

```ts
function assertIsRuleSeverity(ruleId: string, value: unknown): void {
  const severity = ruleSeverities.get(value as SharedConfig.RuleLevel);

  if (severity == null) {
    throw new InvalidRuleSeverityError(ruleId, value);
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Validates that a value is valid rule severity.
 * @param ruleId Rule name being configured.
 * @param value The value to check.
 * @throws {InvalidRuleSeverityError} If the value isn't a valid rule severity.
 */
```

- **Parameters**:
  - `ruleId: string`
  - `value: unknown`
- **Return Type**: `void`
- **Calls**:
  - `ruleSeverities.get`
### `assertIsPluginMemberName(value: unknown): asserts value is PluginMemberName`

<details><summary>Code</summary>

```ts
function assertIsPluginMemberName(
  value: unknown,
): asserts value is PluginMemberName {
  if (typeof value !== 'string' || !/[@\w$-]+(?:\/[\w$-]+)+$/iu.test(value)) {
    throw new TypeError(
      // eslint-disable-next-line @typescript-eslint/restrict-template-expressions
      `Expected string in the form "pluginName/objectName" but found "${value}".`,
    );
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Validates that a given string is the form pluginName/objectName.
 * @param value The string to check.
 */
```

- **Parameters**:
  - `value: unknown`
- **Return Type**: `asserts value is PluginMemberName`
- **Calls**:
  - `/[@\w$-]+(?:\/[\w$-]+)+$/iu.test`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/restrict-template-expressions (x2)
```

### `assertIsObject(value: unknown): void`

<details><summary>Code</summary>

```ts
function assertIsObject(value: unknown): void {
  if (!isNonNullObject(value)) {
    throw new TypeError('Expected an object.');
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Validates that a value is an object.
 * @param value The value to check.
 */
```

- **Parameters**:
  - `value: unknown`
- **Return Type**: `void`
- **Calls**:
  - `isNonNullObject`
### `createEslintrcErrorSchema(key: string): ObjectPropertySchema`

<details><summary>Code</summary>

```ts
function createEslintrcErrorSchema(key: string): ObjectPropertySchema {
  return {
    merge: 'replace',
    validate(): void {
      throw new IncompatibleKeyError(key);
    },
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Creates a schema that always throws an error. Useful for warning
 * about eslintrc-style keys.
 * @param key The eslintrc key to create a schema for.
 */
```

- **Parameters**:
  - `key: string`
- **Return Type**: `ObjectPropertySchema`

---

## Classes

### `InvalidRuleOptionsError`

<details><summary>Class Code</summary>

```ts
class InvalidRuleOptionsError extends Error {
  readonly messageData: { ruleId: string; value: unknown };
  readonly messageTemplate: string;

  constructor(ruleId: string, value: unknown) {
    super(
      `Key "${ruleId}": Expected severity of "off", 0, "warn", 1, "error", or 2.`,
    );
    this.messageTemplate = 'invalid-rule-options';
    this.messageData = { ruleId, value };
  }
}
```
</details>

### `InvalidRuleSeverityError`

<details><summary>Class Code</summary>

```ts
class InvalidRuleSeverityError extends Error {
  readonly messageData: { ruleId: string; value: unknown };
  readonly messageTemplate: string;

  constructor(ruleId: string, value: unknown) {
    super(
      `Key "${ruleId}": Expected severity of "off", 0, "warn", 1, "error", or 2.`,
    );
    this.messageTemplate = 'invalid-rule-severity';
    this.messageData = { ruleId, value };
  }
}
```
</details>

### `IncompatibleKeyError`

<details><summary>Class Code</summary>

```ts
class IncompatibleKeyError extends Error {
  readonly messageData: { key: string };
  readonly messageTemplate: string;

  /**
   * @param key The invalid key.
   */
  constructor(key: string) {
    super(
      'This appears to be in eslintrc format rather than flat config format.',
    );
    this.messageTemplate = 'eslintrc-incompat';
    this.messageData = { key };
  }
}
```
</details>

### `IncompatiblePluginsError`

<details><summary>Class Code</summary>

```ts
class IncompatiblePluginsError extends Error {
  readonly messageData: { plugins: string[] };
  readonly messageTemplate: string;

  constructor(plugins: string[]) {
    super(
      'This appears to be in eslintrc format (array of strings) rather than flat config format (object).',
    );
    this.messageTemplate = 'eslintrc-plugins';
    this.messageData = { plugins };
  }
}
```
</details>


---

## Interfaces

### `ObjectPropertySchema<T = unknown>`

<details><summary>Interface Code</summary>

```ts
interface ObjectPropertySchema<T = unknown> {
  merge: string | ((a: T, b: T) => T);
  validate: string | ((value: unknown) => asserts value is T);
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `merge` | `string | ((a: T, b: T) => T)` | ✗ |  |
| `validate` | `string | ((value: unknown) => asserts value is T)` | ✗ |  |


---

## Type Aliases

### `PluginMemberName`

```ts
type PluginMemberName = `${string}/${string}`;
```

### `ObjectLike`

```ts
type ObjectLike = Record<string, unknown>;
```

### `ConfigRules`

```ts
type ConfigRules = Record<string, SharedConfig.RuleLevelAndOptions>;
```


---