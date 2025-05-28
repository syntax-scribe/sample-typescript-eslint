[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-readonly-parameter-types.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 9 |
| 📊 Variables & Constants | 5 |
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
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/prefer-readonly-parameter-types.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `@typescript-eslint/rule-tester` |
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `InferMessageIdsTypeFromRule` | `../../src/util` |
| `InferOptionsTypeFromRule` | `../../src/util` |
| `rule` | `../../src/rules/prefer-readonly-parameter-types` |
| `readonlynessOptionsDefaults` | `../../src/util` |
| `dedupeTestCases` | `../dedupeTestCases` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      project: './tsconfig.json',
      tsconfigRootDir: rootPath,
    },
  },
})` | ✗ |
| `primitives` | `string[]` | const | `[
  'boolean',
  'true',
  'string',
  "'a'",
  'number',
  '1',
  'symbol',
  'any',
  'unknown',
  'never',
  'null',
  'undefined',
]` | ✗ |
| `arrays` | `string[]` | const | `[
  'readonly string[]',
  'Readonly<string[]>',
  'ReadonlyArray<string>',
  'readonly [string]',
  'Readonly<[string]>',
]` | ✗ |
| `objects` | `string[]` | const | `[
  '{ foo: "" }',
  '{ foo: readonly string[] }',
  '{ foo(): void }',
]` | ✗ |
| `weirdIntersections` | `string[]` | const | `[
  `
    interface Test {
      (): void
      readonly property: boolean
    }
    function foo(arg: Test) {}
  `,
  `
    type Test = (() => void) & {
      readonly property: boolean
    };
    function foo(arg: Test) {}
  `,
]` | ✗ |


---

## 🔧 Functions

> No functions found in this file.


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = InferMessageIdsTypeFromRule<typeof rule>;
```

### `Options`

```ts
type Options = InferOptionsTypeFromRule<typeof rule>;
```


---