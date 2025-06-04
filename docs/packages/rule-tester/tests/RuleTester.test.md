[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `RuleTester.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 78 |
| 📦 Imports | 10 |
| 📊 Variables & Constants | 29 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-tester/tests/RuleTester.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `Linter` | `@typescript-eslint/utils/ts-eslint` |
| `RuleModule` | `@typescript-eslint/utils/ts-eslint` |
| `MockInstance` | `vitest` |
| `AST_NODE_TYPES` | `@typescript-eslint/typescript-estree` |
| `InvalidTestCase` | `../src` |
| `RuleTesterConfig` | `../src` |
| `ValidTestCase` | `../src` |
| `RuleTesterTestFrameworkFunctionBase` | `../src/TestFramework` |
| `RuleTester` | `../src/RuleTester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `dependencyConstraints` | `any` | let/var | `await importOriginal()` | ✗ |
| `actualParser` | `any` | let/var | `await importOriginal()` | ✗ |
| `EMPTY_PROGRAM` | `TSESTree.Program` | const | `{
  body: [],
  comments: [],
  loc: { end: { column: 0, line: 0 }, start: { column: 0, line: 0 } },
  range: [0, 0],
  sourceType: 'module',
  tokens: [],
  type: AST_NODE_TYPES.Program,
}` | ✗ |
| `NOOP_RULE` | `RuleModule<'error'>` | const | `{
  create() {
    return {};
  },
  defaultOptions: [],
  meta: {
    messages: {
      error: 'error',
    },
    schema: [],
    type: 'problem',
  },
}` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester({
        languageOptions: {
          parser,
          parserOptions: {
            project: 'tsconfig.json',
            tsconfigRootDir: '/some/path/that/totally/exists/',
          },
        },
      })` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester({
        defaultFilenames: {
          ts: 'set-in-constructor.ts',
          tsx: 'react-set-in-constructor.tsx',
        },
        languageOptions: {
          parser,
          parserOptions: {
            project: 'tsconfig.json',
            tsconfigRootDir: '/some/path/that/totally/exists/',
          },
        },
      })` | ✗ |
| `callback` | `any` | const | `mockedAfterAll.mock.calls[0][0]` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester({
      linterOptions: {
        reportUnusedDisableDirectives: 0,
      },
    })` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester({
      languageOptions: {
        parser,
        parserOptions: {
          project: 'tsconfig.json',
          tsconfigRootDir: '/some/path/that/totally/exists/',
        },
      },
    })` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester({
        languageOptions: { parser },
      })` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester({
          languageOptions: { parser },
        })` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester({
          languageOptions: { parser },
        })` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester({
        languageOptions: { parser },
      })` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester({
        languageOptions: { parser },
      })` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester({
        languageOptions: { parser },
      })` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester({
          dependencyConstraints: {
            'totally-real-dependency': '999',
          },
          languageOptions: { parser },
        })` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester({
          dependencyConstraints: {
            'totally-real-dependency': '10',
          },
          languageOptions: { parser },
        })` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester()` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester()` | ✗ |
| `noFooRule` | `RuleModule<'error'>` | const | `{
    create(context) {
      return {
        'Identifier[name=foo]'(node): void {
          context.report({
            messageId: 'error',
            node,
          });
        },
      };
    },
    defaultOptions: [],
    meta: {
      messages: {
        error: 'error',
      },
      schema: [],
      type: 'problem',
    },
  }` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester()` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester()` | ✗ |
| `rule` | `RuleModule<'error'>` | const | `{
      create(context) {
        return {
          'Identifier[name=foo]'(node): void {
            context.report({
              messageId: 'error',
              node,
            });
          },
        };
      },
      defaultOptions: [],
      meta: {
        messages: {
          error: 'error',
        },
        schema: [],
        type: 'problem',
      },
    }` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester()` | ✗ |
| `rule` | `RuleModule<'error'>` | const | `{
      create(context) {
        return {
          'Identifier[name=foo]'(node): void {
            context.report({
              fix: fixer => fixer.replaceText(node, 'bar'),
              messageId: 'error',
              node,
            });
          },
        };
      },
      defaultOptions: [],
      meta: {
        fixable: 'code',
        messages: {
          error: 'error',
        },
        schema: [],
        type: 'problem',
      },
    }` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester()` | ✗ |
| `rule` | `RuleModule<'error'>` | const | `{
      create(context) {
        return {
          'Identifier[name=bar]'(node): void {
            context.report({
              fix: fixer => fixer.replaceText(node, 'baz'),
              messageId: 'error',
              node,
            });
          },
          'Identifier[name=foo]'(node): void {
            context.report({
              fix: fixer => fixer.replaceText(node, 'bar'),
              messageId: 'error',
              node,
            });
          },
        };
      },
      defaultOptions: [],
      meta: {
        fixable: 'code',
        messages: {
          error: 'error',
        },
        schema: [],
        type: 'problem',
      },
    }` | ✗ |
| `ruleTester` | `RuleTester` | const | `new RuleTester()` | ✗ |
| `ruleModule` | `RuleModule<
    'customErrorBar' | 'customErrorFoo',
    [{ flag: 'bar' | 'foo' }?]
  >` | const | `{
    create(context) {
      const [{ flag } = {}] = context.options;
      return {
        Identifier(node) {
          if (node.name === 'foo' && flag === 'foo') {
            context.report({ messageId: 'customErrorFoo', node });
          }
          if (node.name === 'bar' && flag === 'bar') {
            context.report({ messageId: 'customErrorBar', node });
          }
        },
      };
    },
    defaultOptions: [],
    meta: {
      messages: {
        customErrorBar: 'Error custom Bar',
        customErrorFoo: 'Error custom Foo',
      },
      schema: [
        {
          additionalProperties: false,
          properties: {
            flag: { enum: ['foo', 'bar'], type: 'string' },
          },
          type: 'object',
        },
      ],
      type: 'suggestion',
    },
  }` | ✗ |


---

## Functions

### `IMMEDIATE_CALLBACK(_: string, cb: () => void): void`

<details><summary>Code</summary>

```ts
(_, cb) => cb()
```
</details>

- **Parameters**:
  - `_: string`
  - `cb: () => void`
- **Return Type**: `void`
- **Calls**:
  - `cb`
### `getTestConfigFromCall(): unknown[]`

<details><summary>Code</summary>

```ts
function getTestConfigFromCall(): unknown[] {
    return runRuleForItemSpy.mock.calls.map(c => {
      return { ...c[2], filename: c[2].filename?.replaceAll('\\', '/') };
    });
  }
```
</details>

- **Return Type**: `unknown[]`
- **Calls**:
  - `runRuleForItemSpy.mock.calls.map`
  - `c[2].filename?.replaceAll`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'baz')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'bar')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `generateValidTestCase(): ValidTestCase<[{ flag: 'foo' }]>`

<details><summary>Code</summary>

```ts
function generateValidTestCase(): ValidTestCase<[{ flag: 'foo' }]> {
      return { code: 'valid' };
    }
```
</details>

- **Return Type**: `ValidTestCase<[{ flag: 'foo' }]>`
### `generateIncompatibleValidTestCase(): ValidTestCase<unknown[]>`

<details><summary>Code</summary>

```ts
function generateIncompatibleValidTestCase(): ValidTestCase<unknown[]> {
      return { code: 'validIncompatible' };
    }
```
</details>

- **Return Type**: `ValidTestCase<unknown[]>`
### `generateInvalidTestCase(): InvalidTestCase<
      'customErrorBar',
      [{ flag: 'bar' }]
    >`

<details><summary>Code</summary>

```ts
function generateInvalidTestCase(): InvalidTestCase<
      'customErrorBar',
      [{ flag: 'bar' }]
    > {
      return {
        code: 'bar',
        errors: [{ messageId: 'customErrorBar' }],
        options: [{ flag: 'bar' }],
      };
    }
```
</details>

- **Return Type**: `InvalidTestCase<
      'customErrorBar',
      [{ flag: 'bar' }]
    >`
### `generateIncompatibleInvalidTestCase(): InvalidTestCase<
      'customErrorBar' | 'customErrorBaz',
      unknown[]
    >`

<details><summary>Code</summary>

```ts
function generateIncompatibleInvalidTestCase(): InvalidTestCase<
      'customErrorBar' | 'customErrorBaz',
      unknown[]
    > {
      return {
        code: 'let bar',
        errors: [{ messageId: 'customErrorBar' }],
        options: [{ flag: 'bar' }],
      };
    }
```
</details>

- **Return Type**: `InvalidTestCase<
      'customErrorBar' | 'customErrorBaz',
      unknown[]
    >`

---