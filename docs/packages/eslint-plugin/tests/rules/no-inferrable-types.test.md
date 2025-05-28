[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-inferrable-types.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 2 |
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
📂 **`packages/eslint-plugin/tests/rules/no-inferrable-types.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `InferMessageIdsTypeFromRule` | `../../src/util` |
| `InferOptionsTypeFromRule` | `../../src/util` |
| `rule` | `../../src/rules/no-inferrable-types` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `testCases` | `{ code: string[]; type: string; }[]` | const | `[
  {
    code: [
      '10n',
      '-10n',
      'BigInt(10)',
      '-BigInt(10)',
      'BigInt?.(10)',
      '-BigInt?.(10)',
    ],
    type: 'bigint',
  },
  {
    code: ['false', 'true', 'Boolean(null)', 'Boolean?.(null)', '!0'],
    type: 'boolean',
  },
  {
    code: [
      '10',
      '+10',
      '-10',
      'Number("1")',
      '+Number("1")',
      '-Number("1")',
      'Number?.("1")',
      '+Number?.("1")',
      '-Number?.("1")',
      'Infinity',
      '+Infinity',
      '-Infinity',
      'NaN',
      '+NaN',
      '-NaN',
    ],
    type: 'number',
  },
  {
    code: ['null'],
    type: 'null',
  },
  {
    code: ['/a/', 'RegExp("a")', 'RegExp?.("a")', 'new RegExp("a")'],
    type: 'RegExp',
  },
  {
    code: ['"str"', "'str'", '`str`', 'String(1)', 'String?.(1)'],
    type: 'string',
  },
  {
    code: ['Symbol("a")', 'Symbol?.("a")'],
    type: 'symbol',
  },
  {
    code: ['undefined', 'void someValue'],
    type: 'undefined',
  },
]` | ✗ |
| `ruleTester` | `any` | const | `new RuleTester()` | ✗ |


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