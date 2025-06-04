[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `TestFramework.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📊 Variables & Constants | 9 |
| 📑 Type Aliases | 5 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Classes](#classes)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/TestFramework.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `describe` | `RuleTesterTestFrameworkFunction | undefined` | let/var | `*not shown*` | ✗ |
| `it` | `RuleTesterTestFrameworkItFunction | undefined` | let/var | `*not shown*` | ✗ |
| `afterAll` | `AfterAll | undefined` | let/var | `*not shown*` | ✗ |
| `OVERRIDE_AFTER_ALL` | `Maybe<AfterAll>` | let/var | `null` | ✗ |
| `OVERRIDE_DESCRIBE` | `Maybe<RuleTesterTestFrameworkFunction>` | let/var | `null` | ✗ |
| `OVERRIDE_DESCRIBE_SKIP` | `Maybe<RuleTesterTestFrameworkFunctionBase>` | let/var | `null` | ✗ |
| `OVERRIDE_IT` | `Maybe<RuleTesterTestFrameworkItFunction>` | let/var | `null` | ✗ |
| `OVERRIDE_IT_ONLY` | `Maybe<RuleTesterTestFrameworkFunctionBase>` | let/var | `null` | ✗ |
| `OVERRIDE_IT_SKIP` | `Maybe<RuleTesterTestFrameworkFunctionBase>` | let/var | `null` | ✗ |


---

## Classes

### `TestFramework`

<details><summary>Class Code</summary>

```ts
export abstract class TestFramework {
  /**
   * Runs a function after all the tests in this file have completed.
   */
  static get afterAll(): AfterAll {
    if (OVERRIDE_AFTER_ALL != null) {
      return OVERRIDE_AFTER_ALL;
    }
    if (typeof afterAll === 'function') {
      return afterAll;
    }
    throw new Error(
      'Missing definition for `afterAll` - you must set one using `RuleTester.afterAll` or there must be one defined globally as `afterAll`.',
    );
  }
  static set afterAll(value: Maybe<AfterAll>) {
    OVERRIDE_AFTER_ALL = value;
  }

  /**
   * Creates a test grouping
   */
  static get describe(): RuleTesterTestFrameworkFunction {
    if (OVERRIDE_DESCRIBE != null) {
      return OVERRIDE_DESCRIBE;
    }
    if (typeof describe === 'function') {
      return describe;
    }
    throw new Error(
      'Missing definition for `describe` - you must set one using `RuleTester.describe` or there must be one defined globally as `describe`.',
    );
  }
  static set describe(value: Maybe<RuleTesterTestFrameworkFunction>) {
    OVERRIDE_DESCRIBE = value;
  }

  /**
   * Skips running the tests inside this `describe` for the current file
   */
  static get describeSkip(): RuleTesterTestFrameworkFunctionBase {
    if (OVERRIDE_DESCRIBE_SKIP != null) {
      return OVERRIDE_DESCRIBE_SKIP;
    }
    if (
      typeof OVERRIDE_DESCRIBE === 'function' &&
      typeof OVERRIDE_DESCRIBE.skip === 'function'
    ) {
      return OVERRIDE_DESCRIBE.skip.bind(OVERRIDE_DESCRIBE);
    }
    if (typeof describe === 'function' && typeof describe.skip === 'function') {
      return describe.skip.bind(describe);
    }
    if (
      typeof OVERRIDE_DESCRIBE === 'function' ||
      typeof OVERRIDE_IT === 'function'
    ) {
      throw new Error(
        'Set `RuleTester.describeSkip` to use `dependencyConstraints` with a custom test framework.',
      );
    }
    if (typeof describe === 'function') {
      throw new Error(
        'The current test framework does not support skipping tests tests with `dependencyConstraints`.',
      );
    }
    throw new Error(
      'Missing definition for `describeSkip` - you must set one using `RuleTester.describeSkip` or there must be one defined globally as `describe.skip`.',
    );
  }
  static set describeSkip(value: Maybe<RuleTesterTestFrameworkFunctionBase>) {
    OVERRIDE_DESCRIBE_SKIP = value;
  }

  /**
   * Creates a test closure
   */
  static get it(): RuleTesterTestFrameworkItFunction {
    if (OVERRIDE_IT != null) {
      return OVERRIDE_IT;
    }
    if (typeof it === 'function') {
      return it;
    }
    throw new Error(
      'Missing definition for `it` - you must set one using `RuleTester.it` or there must be one defined globally as `it`.',
    );
  }
  static set it(value: Maybe<RuleTesterTestFrameworkItFunction>) {
    OVERRIDE_IT = value;
  }

  /**
   * Only runs this test in the current file.
   */
  static get itOnly(): RuleTesterTestFrameworkFunctionBase {
    if (OVERRIDE_IT_ONLY != null) {
      return OVERRIDE_IT_ONLY;
    }
    if (
      typeof OVERRIDE_IT === 'function' &&
      typeof OVERRIDE_IT.only === 'function'
    ) {
      return OVERRIDE_IT.only.bind(OVERRIDE_IT);
    }
    if (typeof it === 'function' && typeof it.only === 'function') {
      return it.only.bind(it);
    }
    if (
      typeof OVERRIDE_DESCRIBE === 'function' ||
      typeof OVERRIDE_IT === 'function'
    ) {
      throw new Error(
        'Set `RuleTester.itOnly` to use `only` with a custom test framework.\n' +
          'See https://eslint.org/docs/latest/integrate/nodejs-api#customizing-ruletester for more.',
      );
    }
    if (typeof it === 'function') {
      throw new Error(
        'The current test framework does not support exclusive tests with `only`.',
      );
    }
    throw new Error(
      'Missing definition for `itOnly` - you must set one using `RuleTester.itOnly` or there must be one defined globally as `it.only`.',
    );
  }
  static set itOnly(value: Maybe<RuleTesterTestFrameworkFunctionBase>) {
    OVERRIDE_IT_ONLY = value;
  }

  /**
   * Skips running this test in the current file.
   */
  static get itSkip(): RuleTesterTestFrameworkFunctionBase {
    if (OVERRIDE_IT_SKIP != null) {
      return OVERRIDE_IT_SKIP;
    }
    if (
      typeof OVERRIDE_IT === 'function' &&
      typeof OVERRIDE_IT.skip === 'function'
    ) {
      return OVERRIDE_IT.skip.bind(OVERRIDE_IT);
    }
    if (typeof it === 'function' && typeof it.skip === 'function') {
      return it.skip.bind(it);
    }
    if (
      typeof OVERRIDE_DESCRIBE === 'function' ||
      typeof OVERRIDE_IT === 'function'
    ) {
      throw new Error(
        'Set `RuleTester.itSkip` to use `only` with a custom test framework.',
      );
    }
    if (typeof it === 'function') {
      throw new Error(
        'The current test framework does not support exclusive tests with `only`.',
      );
    }
    throw new Error(
      'Missing definition for `itSkip` - you must set one using `RuleTester.itSkip` or there must be one defined globally as `it.only`.',
    );
  }
  static set itSkip(value: Maybe<RuleTesterTestFrameworkFunctionBase>) {
    OVERRIDE_IT_SKIP = value;
  }
}
```
</details>


---

## Type Aliases

### `RuleTesterTestFrameworkFunctionBase`

/**
 * @param text a string describing the rule
 */

```ts
type RuleTesterTestFrameworkFunctionBase = (
  text: string,
  callback: () => void,
) => void;
```

### `RuleTesterTestFrameworkFunction`

```ts
type RuleTesterTestFrameworkFunction = {
  /**
   * Skips running the tests inside this `describe` for the current file
   */
  skip?: RuleTesterTestFrameworkFunctionBase;
} & RuleTesterTestFrameworkFunctionBase;
```

### `RuleTesterTestFrameworkItFunction`

```ts
type RuleTesterTestFrameworkItFunction = {
  /**
   * Only runs this test in the current file.
   */
  only?: RuleTesterTestFrameworkFunctionBase;
  /**
   * Skips running this test in the current file.
   */
  skip?: RuleTesterTestFrameworkFunctionBase;
} & RuleTesterTestFrameworkFunctionBase;
```

### `Maybe<T>`

```ts
type Maybe<T> = T | null | undefined;
```

### `AfterAll`

/**
 * @param fn a callback called after all the tests are done
 */

```ts
type AfterAll = (fn: () => void) => void;
```


---