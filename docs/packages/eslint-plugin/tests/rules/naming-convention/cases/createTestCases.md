[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `createTestCases.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |
| 📦 Imports | 9 |
| 📊 Variables & Constants | 13 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/naming-convention/cases/createTestCases.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `@typescript-eslint/rule-tester` |
| `ValidTestCase` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `MessageIds` | `../../../../src/rules/naming-convention` |
| `Options` | `../../../../src/rules/naming-convention` |
| `PredefinedFormatsString` | `../../../../src/rules/naming-convention-utils` |
| `Selector` | `../../../../src/rules/naming-convention-utils` |
| `rule` | `../../../../src/rules/naming-convention` |
| `selectorTypeToMessageString` | `../../../../src/rules/naming-convention-utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `formatTestNames` | `Readonly<
  Record<PredefinedFormatsString, Record<'invalid' | 'valid', string[]>>
>` | const | `{
  camelCase: {
    invalid: ['snake_case', 'UPPER_CASE', 'UPPER', 'StrictPascalCase'],
    valid: ['strictCamelCase', 'lower', 'camelCaseUNSTRICT'],
  },
  PascalCase: {
    invalid: ['snake_case', 'UPPER_CASE', 'strictCamelCase'],
    valid: [
      'StrictPascalCase',
      'Pascal',
      'I18n',
      'PascalCaseUNSTRICT',
      'UPPER',
    ],
  },
  snake_case: {
    invalid: [
      'UPPER_CASE',
      'SNAKE_case_UNSTRICT',
      'strictCamelCase',
      'StrictPascalCase',
    ],
    valid: ['snake_case', 'lower'],
  },
  strictCamelCase: {
    invalid: [
      'snake_case',
      'UPPER_CASE',
      'UPPER',
      'StrictPascalCase',
      'camelCaseUNSTRICT',
    ],
    valid: ['strictCamelCase', 'lower'],
  },
  StrictPascalCase: {
    invalid: [
      'snake_case',
      'UPPER_CASE',
      'UPPER',
      'strictCamelCase',
      'PascalCaseUNSTRICT',
    ],
    valid: ['StrictPascalCase', 'Pascal', 'I18n'],
  },
  UPPER_CASE: {
    invalid: [
      'lower',
      'snake_case',
      'SNAKE_case_UNSTRICT',
      'strictCamelCase',
      'StrictPascalCase',
    ],
    valid: ['UPPER_CASE', 'UPPER'],
  },
}` | ✓ |
| `REPLACE_REGEX` | `RegExp` | const | `/%/g` | ✗ |
| `IGNORED_FILTER` | `{ match: boolean; regex: string; }` | const | `{
  match: false,
  regex: /.gnored/.source,
}` | ✗ |
| `format` | `("camelCase" | "strictCamelCase" | "PascalCase" | "StrictPascalCase" | "snake_case" | "UPPER_CASE")[]` | const | `[formatLoose as PredefinedFormatsString]` | ✗ |
| `newCases` | `InvalidTestCase<MessageIds, Options>[]` | const | `[]` | ✗ |
| `format` | `("camelCase" | "strictCamelCase" | "PascalCase" | "StrictPascalCase" | "snake_case" | "UPPER_CASE")[]` | const | `[formatLoose as PredefinedFormatsString]` | ✗ |
| `selectors` | `IndividualAndMetaSelectorsString[]` | const | `Array.isArray(test.options.selector)
              ? test.options.selector
              : [test.options.selector]` | ✗ |
| `errors` | `{
              data?: { name: string; type: string };
              messageId: MessageIds;
            }[]` | const | `[]` | ✗ |
| `prefixSingle` | `string[]` | const | `['MyPrefix']` | ✗ |
| `prefixMulti` | `string[]` | const | `['MyPrefix1', 'MyPrefix2']` | ✗ |
| `suffixSingle` | `string[]` | const | `['MySuffix']` | ✗ |
| `suffixMulti` | `string[]` | const | `['MySuffix1', 'MySuffix2']` | ✗ |
| `ruleTester` | `any` | const | `new RuleTester()` | ✗ |


---

## Functions

### `createTestCases(cases: Cases): void`

<details><summary>Code</summary>

```ts
export function createTestCases(cases: Cases): void {
  const createValidTestCases = (): ValidTestCase<Options>[] =>
    cases.flatMap(test =>
      Object.entries(formatTestNames).flatMap(([formatLoose, names]) =>
        names.valid.flatMap(name => {
          const format = [formatLoose as PredefinedFormatsString];
          const createCase = (
            preparedName: string,
            options: Selector,
          ): ValidTestCase<Options> => ({
            code: `// ${JSON.stringify(options)}\n${test.code
              .map(code => code.replaceAll(REPLACE_REGEX, preparedName))
              .join('\n')}`,
            options: [{ ...options, filter: IGNORED_FILTER }],
          });

          return [
            createCase(name, { ...test.options, format }),

            // leadingUnderscore
            createCase(name, {
              ...test.options,
              format,
              leadingUnderscore: 'forbid',
            }),
            createCase(`_${name}`, {
              ...test.options,
              format,
              leadingUnderscore: 'require',
            }),
            createCase(`__${name}`, {
              ...test.options,
              format,
              leadingUnderscore: 'requireDouble',
            }),
            createCase(`_${name}`, {
              ...test.options,
              format,
              leadingUnderscore: 'allow',
            }),
            createCase(name, {
              ...test.options,
              format,
              leadingUnderscore: 'allow',
            }),
            createCase(`__${name}`, {
              ...test.options,
              format,
              leadingUnderscore: 'allowDouble',
            }),
            createCase(name, {
              ...test.options,
              format,
              leadingUnderscore: 'allowDouble',
            }),
            createCase(`_${name}`, {
              ...test.options,
              format,
              leadingUnderscore: 'allowSingleOrDouble',
            }),
            createCase(name, {
              ...test.options,
              format,
              leadingUnderscore: 'allowSingleOrDouble',
            }),
            createCase(`__${name}`, {
              ...test.options,
              format,
              leadingUnderscore: 'allowSingleOrDouble',
            }),

            // trailingUnderscore
            createCase(name, {
              ...test.options,
              format,
              trailingUnderscore: 'forbid',
            }),
            createCase(`${name}_`, {
              ...test.options,
              format,
              trailingUnderscore: 'require',
            }),
            createCase(`${name}__`, {
              ...test.options,
              format,
              trailingUnderscore: 'requireDouble',
            }),
            createCase(`${name}_`, {
              ...test.options,
              format,
              trailingUnderscore: 'allow',
            }),
            createCase(name, {
              ...test.options,
              format,
              trailingUnderscore: 'allow',
            }),
            createCase(`${name}__`, {
              ...test.options,
              format,
              trailingUnderscore: 'allowDouble',
            }),
            createCase(name, {
              ...test.options,
              format,
              trailingUnderscore: 'allowDouble',
            }),
            createCase(`${name}_`, {
              ...test.options,
              format,
              trailingUnderscore: 'allowSingleOrDouble',
            }),
            createCase(name, {
              ...test.options,
              format,
              trailingUnderscore: 'allowSingleOrDouble',
            }),
            createCase(`${name}__`, {
              ...test.options,
              format,
              trailingUnderscore: 'allowSingleOrDouble',
            }),

            // prefix
            createCase(`MyPrefix${name}`, {
              ...test.options,
              format,
              prefix: ['MyPrefix'],
            }),
            createCase(`MyPrefix2${name}`, {
              ...test.options,
              format,
              prefix: ['MyPrefix1', 'MyPrefix2'],
            }),

            // suffix
            createCase(`${name}MySuffix`, {
              ...test.options,
              format,
              suffix: ['MySuffix'],
            }),
            createCase(`${name}MySuffix2`, {
              ...test.options,
              format,
              suffix: ['MySuffix1', 'MySuffix2'],
            }),
          ];
        }),
      ),
    );

  function createInvalidTestCases(): InvalidTestCase<MessageIds, Options>[] {
    const newCases: InvalidTestCase<MessageIds, Options>[] = [];

    for (const test of cases) {
      for (const [formatLoose, names] of Object.entries(formatTestNames)) {
        const format = [formatLoose as PredefinedFormatsString];
        for (const name of names.invalid) {
          const createCase = (
            preparedName: string,
            options: Selector,
            messageId: MessageIds,
            data: Record<string, unknown> = {},
          ): InvalidTestCase<MessageIds, Options> => {
            const selectors = Array.isArray(test.options.selector)
              ? test.options.selector
              : [test.options.selector];
            const errorsTemplate = selectors.map(selector => ({
              messageId,
              ...(selector !== 'default' &&
              selector !== 'variableLike' &&
              selector !== 'memberLike' &&
              selector !== 'typeLike' &&
              selector !== 'property' &&
              selector !== 'method' &&
              selector !== 'accessor'
                ? {
                    data: {
                      name: preparedName,
                      type: selectorTypeToMessageString(selector),
                      ...data,
                    },
                  }
                : // meta-types will use the correct selector, so don't assert on data shape
                  {}),
            }));

            const errors: {
              data?: { name: string; type: string };
              messageId: MessageIds;
            }[] = [];
            test.code.forEach(() => errors.push(...errorsTemplate));

            return {
              code: `// ${JSON.stringify(options)}\n${test.code
                .map(code => code.replaceAll(REPLACE_REGEX, preparedName))
                .join('\n')}`,
              errors,
              options: [
                {
                  ...options,
                  filter: IGNORED_FILTER,
                },
              ],
            };
          };

          const prefixSingle = ['MyPrefix'];
          const prefixMulti = ['MyPrefix1', 'MyPrefix2'];
          const suffixSingle = ['MySuffix'];
          const suffixMulti = ['MySuffix1', 'MySuffix2'];

          newCases.push(
            createCase(
              name,
              {
                ...test.options,
                format,
              },
              'doesNotMatchFormat',
              { formats: format.join(', ') },
            ),

            // leadingUnderscore
            createCase(
              `_${name}`,
              {
                ...test.options,
                format,
                leadingUnderscore: 'forbid',
              },
              'unexpectedUnderscore',
              { position: 'leading' },
            ),
            createCase(
              name,
              {
                ...test.options,
                format,
                leadingUnderscore: 'require',
              },
              'missingUnderscore',
              { count: 'one', position: 'leading' },
            ),
            createCase(
              name,
              {
                ...test.options,
                format,
                leadingUnderscore: 'requireDouble',
              },
              'missingUnderscore',
              { count: 'two', position: 'leading' },
            ),
            createCase(
              `_${name}`,
              {
                ...test.options,
                format,
                leadingUnderscore: 'requireDouble',
              },
              'missingUnderscore',
              { count: 'two', position: 'leading' },
            ),

            // trailingUnderscore
            createCase(
              `${name}_`,
              {
                ...test.options,
                format,
                trailingUnderscore: 'forbid',
              },
              'unexpectedUnderscore',
              { position: 'trailing' },
            ),
            createCase(
              name,
              {
                ...test.options,
                format,
                trailingUnderscore: 'require',
              },
              'missingUnderscore',
              { count: 'one', position: 'trailing' },
            ),
            createCase(
              name,
              {
                ...test.options,
                format,
                trailingUnderscore: 'requireDouble',
              },
              'missingUnderscore',
              { count: 'two', position: 'trailing' },
            ),
            createCase(
              `${name}_`,
              {
                ...test.options,
                format,
                trailingUnderscore: 'requireDouble',
              },
              'missingUnderscore',
              { count: 'two', position: 'trailing' },
            ),

            // prefix
            createCase(
              name,
              {
                ...test.options,
                format,
                prefix: prefixSingle,
              },
              'missingAffix',
              { affixes: prefixSingle.join(', '), position: 'prefix' },
            ),
            createCase(
              name,
              {
                ...test.options,
                format,
                prefix: prefixMulti,
              },
              'missingAffix',
              {
                affixes: prefixMulti.join(', '),
                position: 'prefix',
              },
            ),

            // suffix
            createCase(
              name,
              {
                ...test.options,
                format,
                suffix: suffixSingle,
              },
              'missingAffix',
              { affixes: suffixSingle.join(', '), position: 'suffix' },
            ),
            createCase(
              name,
              {
                ...test.options,
                format,
                suffix: suffixMulti,
              },
              'missingAffix',
              {
                affixes: suffixMulti.join(', '),
                position: 'suffix',
              },
            ),
          );
        }
      }
    }

    return newCases;
  }

  const ruleTester = new RuleTester();

  ruleTester.run('naming-convention', rule, {
    invalid: createInvalidTestCases(),
    valid: createValidTestCases(),
  });
}
```
</details>

- **Parameters**:
  - `cases: Cases`
- **Return Type**: `void`
- **Calls**:
  - `cases.flatMap`
  - `Object.entries(formatTestNames).flatMap`
  - `names.valid.flatMap`
  - `JSON.stringify`
  - `test.code
              .map(code => code.replaceAll(REPLACE_REGEX, preparedName))
              .join`
  - `createCase`
  - `Object.entries`
  - `Array.isArray`
  - `selectors.map`
  - `selectorTypeToMessageString (from ../../../../src/rules/naming-convention-utils)`
  - `test.code.forEach`
  - `errors.push`
  - `test.code
                .map(code => code.replaceAll(REPLACE_REGEX, preparedName))
                .join`
  - `newCases.push`
  - `format.join`
  - `prefixSingle.join`
  - `prefixMulti.join`
  - `suffixSingle.join`
  - `suffixMulti.join`
  - `ruleTester.run`
  - `createInvalidTestCases`
  - `createValidTestCases`
- **Internal Comments**:
```
// leadingUnderscore (x4)
// trailingUnderscore (x4)
// prefix (x4)
// suffix (x4)
```

### `createValidTestCases(): ValidTestCase<Options>[]`

<details><summary>Code</summary>

```ts
(): ValidTestCase<Options>[] =>
    cases.flatMap(test =>
      Object.entries(formatTestNames).flatMap(([formatLoose, names]) =>
        names.valid.flatMap(name => {
          const format = [formatLoose as PredefinedFormatsString];
          const createCase = (
            preparedName: string,
            options: Selector,
          ): ValidTestCase<Options> => ({
            code: `// ${JSON.stringify(options)}\n${test.code
              .map(code => code.replaceAll(REPLACE_REGEX, preparedName))
              .join('\n')}`,
            options: [{ ...options, filter: IGNORED_FILTER }],
          });

          return [
            createCase(name, { ...test.options, format }),

            // leadingUnderscore
            createCase(name, {
              ...test.options,
              format,
              leadingUnderscore: 'forbid',
            }),
            createCase(`_${name}`, {
              ...test.options,
              format,
              leadingUnderscore: 'require',
            }),
            createCase(`__${name}`, {
              ...test.options,
              format,
              leadingUnderscore: 'requireDouble',
            }),
            createCase(`_${name}`, {
              ...test.options,
              format,
              leadingUnderscore: 'allow',
            }),
            createCase(name, {
              ...test.options,
              format,
              leadingUnderscore: 'allow',
            }),
            createCase(`__${name}`, {
              ...test.options,
              format,
              leadingUnderscore: 'allowDouble',
            }),
            createCase(name, {
              ...test.options,
              format,
              leadingUnderscore: 'allowDouble',
            }),
            createCase(`_${name}`, {
              ...test.options,
              format,
              leadingUnderscore: 'allowSingleOrDouble',
            }),
            createCase(name, {
              ...test.options,
              format,
              leadingUnderscore: 'allowSingleOrDouble',
            }),
            createCase(`__${name}`, {
              ...test.options,
              format,
              leadingUnderscore: 'allowSingleOrDouble',
            }),

            // trailingUnderscore
            createCase(name, {
              ...test.options,
              format,
              trailingUnderscore: 'forbid',
            }),
            createCase(`${name}_`, {
              ...test.options,
              format,
              trailingUnderscore: 'require',
            }),
            createCase(`${name}__`, {
              ...test.options,
              format,
              trailingUnderscore: 'requireDouble',
            }),
            createCase(`${name}_`, {
              ...test.options,
              format,
              trailingUnderscore: 'allow',
            }),
            createCase(name, {
              ...test.options,
              format,
              trailingUnderscore: 'allow',
            }),
            createCase(`${name}__`, {
              ...test.options,
              format,
              trailingUnderscore: 'allowDouble',
            }),
            createCase(name, {
              ...test.options,
              format,
              trailingUnderscore: 'allowDouble',
            }),
            createCase(`${name}_`, {
              ...test.options,
              format,
              trailingUnderscore: 'allowSingleOrDouble',
            }),
            createCase(name, {
              ...test.options,
              format,
              trailingUnderscore: 'allowSingleOrDouble',
            }),
            createCase(`${name}__`, {
              ...test.options,
              format,
              trailingUnderscore: 'allowSingleOrDouble',
            }),

            // prefix
            createCase(`MyPrefix${name}`, {
              ...test.options,
              format,
              prefix: ['MyPrefix'],
            }),
            createCase(`MyPrefix2${name}`, {
              ...test.options,
              format,
              prefix: ['MyPrefix1', 'MyPrefix2'],
            }),

            // suffix
            createCase(`${name}MySuffix`, {
              ...test.options,
              format,
              suffix: ['MySuffix'],
            }),
            createCase(`${name}MySuffix2`, {
              ...test.options,
              format,
              suffix: ['MySuffix1', 'MySuffix2'],
            }),
          ];
        }),
      ),
    )
```
</details>

- **Return Type**: `ValidTestCase<Options>[]`
- **Calls**:
  - `cases.flatMap`
### `createCase(preparedName: string, options: Selector): ValidTestCase<Options>`

<details><summary>Code</summary>

```ts
(
            preparedName: string,
            options: Selector,
          ): ValidTestCase<Options> => ({
            code: `// ${JSON.stringify(options)}\n${test.code
              .map(code => code.replaceAll(REPLACE_REGEX, preparedName))
              .join('\n')}`,
            options: [{ ...options, filter: IGNORED_FILTER }],
          })
```
</details>

- **Parameters**:
  - `preparedName: string`
  - `options: Selector`
- **Return Type**: `ValidTestCase<Options>`
### `createInvalidTestCases(): InvalidTestCase<MessageIds, Options>[]`

<details><summary>Code</summary>

```ts
function createInvalidTestCases(): InvalidTestCase<MessageIds, Options>[] {
    const newCases: InvalidTestCase<MessageIds, Options>[] = [];

    for (const test of cases) {
      for (const [formatLoose, names] of Object.entries(formatTestNames)) {
        const format = [formatLoose as PredefinedFormatsString];
        for (const name of names.invalid) {
          const createCase = (
            preparedName: string,
            options: Selector,
            messageId: MessageIds,
            data: Record<string, unknown> = {},
          ): InvalidTestCase<MessageIds, Options> => {
            const selectors = Array.isArray(test.options.selector)
              ? test.options.selector
              : [test.options.selector];
            const errorsTemplate = selectors.map(selector => ({
              messageId,
              ...(selector !== 'default' &&
              selector !== 'variableLike' &&
              selector !== 'memberLike' &&
              selector !== 'typeLike' &&
              selector !== 'property' &&
              selector !== 'method' &&
              selector !== 'accessor'
                ? {
                    data: {
                      name: preparedName,
                      type: selectorTypeToMessageString(selector),
                      ...data,
                    },
                  }
                : // meta-types will use the correct selector, so don't assert on data shape
                  {}),
            }));

            const errors: {
              data?: { name: string; type: string };
              messageId: MessageIds;
            }[] = [];
            test.code.forEach(() => errors.push(...errorsTemplate));

            return {
              code: `// ${JSON.stringify(options)}\n${test.code
                .map(code => code.replaceAll(REPLACE_REGEX, preparedName))
                .join('\n')}`,
              errors,
              options: [
                {
                  ...options,
                  filter: IGNORED_FILTER,
                },
              ],
            };
          };

          const prefixSingle = ['MyPrefix'];
          const prefixMulti = ['MyPrefix1', 'MyPrefix2'];
          const suffixSingle = ['MySuffix'];
          const suffixMulti = ['MySuffix1', 'MySuffix2'];

          newCases.push(
            createCase(
              name,
              {
                ...test.options,
                format,
              },
              'doesNotMatchFormat',
              { formats: format.join(', ') },
            ),

            // leadingUnderscore
            createCase(
              `_${name}`,
              {
                ...test.options,
                format,
                leadingUnderscore: 'forbid',
              },
              'unexpectedUnderscore',
              { position: 'leading' },
            ),
            createCase(
              name,
              {
                ...test.options,
                format,
                leadingUnderscore: 'require',
              },
              'missingUnderscore',
              { count: 'one', position: 'leading' },
            ),
            createCase(
              name,
              {
                ...test.options,
                format,
                leadingUnderscore: 'requireDouble',
              },
              'missingUnderscore',
              { count: 'two', position: 'leading' },
            ),
            createCase(
              `_${name}`,
              {
                ...test.options,
                format,
                leadingUnderscore: 'requireDouble',
              },
              'missingUnderscore',
              { count: 'two', position: 'leading' },
            ),

            // trailingUnderscore
            createCase(
              `${name}_`,
              {
                ...test.options,
                format,
                trailingUnderscore: 'forbid',
              },
              'unexpectedUnderscore',
              { position: 'trailing' },
            ),
            createCase(
              name,
              {
                ...test.options,
                format,
                trailingUnderscore: 'require',
              },
              'missingUnderscore',
              { count: 'one', position: 'trailing' },
            ),
            createCase(
              name,
              {
                ...test.options,
                format,
                trailingUnderscore: 'requireDouble',
              },
              'missingUnderscore',
              { count: 'two', position: 'trailing' },
            ),
            createCase(
              `${name}_`,
              {
                ...test.options,
                format,
                trailingUnderscore: 'requireDouble',
              },
              'missingUnderscore',
              { count: 'two', position: 'trailing' },
            ),

            // prefix
            createCase(
              name,
              {
                ...test.options,
                format,
                prefix: prefixSingle,
              },
              'missingAffix',
              { affixes: prefixSingle.join(', '), position: 'prefix' },
            ),
            createCase(
              name,
              {
                ...test.options,
                format,
                prefix: prefixMulti,
              },
              'missingAffix',
              {
                affixes: prefixMulti.join(', '),
                position: 'prefix',
              },
            ),

            // suffix
            createCase(
              name,
              {
                ...test.options,
                format,
                suffix: suffixSingle,
              },
              'missingAffix',
              { affixes: suffixSingle.join(', '), position: 'suffix' },
            ),
            createCase(
              name,
              {
                ...test.options,
                format,
                suffix: suffixMulti,
              },
              'missingAffix',
              {
                affixes: suffixMulti.join(', '),
                position: 'suffix',
              },
            ),
          );
        }
      }
    }

    return newCases;
  }
```
</details>

- **Return Type**: `InvalidTestCase<MessageIds, Options>[]`
- **Calls**:
  - `Object.entries`
  - `Array.isArray`
  - `selectors.map`
  - `selectorTypeToMessageString (from ../../../../src/rules/naming-convention-utils)`
  - `test.code.forEach`
  - `errors.push`
  - `JSON.stringify`
  - `test.code
                .map(code => code.replaceAll(REPLACE_REGEX, preparedName))
                .join`
  - `newCases.push`
  - `createCase`
  - `format.join`
  - `prefixSingle.join`
  - `prefixMulti.join`
  - `suffixSingle.join`
  - `suffixMulti.join`
- **Internal Comments**:
```
// leadingUnderscore (x2)
// trailingUnderscore (x2)
// prefix (x2)
// suffix (x2)
```

### `createCase(preparedName: string, options: Selector, messageId: MessageIds, data: Record<string, unknown>): InvalidTestCase<MessageIds, Options>`

<details><summary>Code</summary>

```ts
(
            preparedName: string,
            options: Selector,
            messageId: MessageIds,
            data: Record<string, unknown> = {},
          ): InvalidTestCase<MessageIds, Options> => {
            const selectors = Array.isArray(test.options.selector)
              ? test.options.selector
              : [test.options.selector];
            const errorsTemplate = selectors.map(selector => ({
              messageId,
              ...(selector !== 'default' &&
              selector !== 'variableLike' &&
              selector !== 'memberLike' &&
              selector !== 'typeLike' &&
              selector !== 'property' &&
              selector !== 'method' &&
              selector !== 'accessor'
                ? {
                    data: {
                      name: preparedName,
                      type: selectorTypeToMessageString(selector),
                      ...data,
                    },
                  }
                : // meta-types will use the correct selector, so don't assert on data shape
                  {}),
            }));

            const errors: {
              data?: { name: string; type: string };
              messageId: MessageIds;
            }[] = [];
            test.code.forEach(() => errors.push(...errorsTemplate));

            return {
              code: `// ${JSON.stringify(options)}\n${test.code
                .map(code => code.replaceAll(REPLACE_REGEX, preparedName))
                .join('\n')}`,
              errors,
              options: [
                {
                  ...options,
                  filter: IGNORED_FILTER,
                },
              ],
            };
          }
```
</details>

- **Parameters**:
  - `preparedName: string`
  - `options: Selector`
  - `messageId: MessageIds`
  - `data: Record<string, unknown>`
- **Return Type**: `InvalidTestCase<MessageIds, Options>`
- **Calls**:
  - `Array.isArray`
  - `selectors.map`
  - `selectorTypeToMessageString (from ../../../../src/rules/naming-convention-utils)`
  - `test.code.forEach`
  - `errors.push`
  - `JSON.stringify`
  - `test.code
                .map(code => code.replaceAll(REPLACE_REGEX, preparedName))
                .join`

---

## Type Aliases

### `Cases`

```ts
type Cases = { code: string[]; options: Omit<Options[0], 'format'> }[];
```


---