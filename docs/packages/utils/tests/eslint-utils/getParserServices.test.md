[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getParserServices.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/utils/tests/eslint-utils/getParserServices.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserServices` | `../../src` |
| `TSESLint` | `../../src` |
| `TSESTree` | `../../src` |
| `FlatConfig` | `../../src/ts-eslint` |
| `ESLintUtils` | `../../src` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `defaults` | `Readonly<RuleContext<string, unknown[]>>` | const | `{
  parserPath: '@typescript-eslint/parser/dist/index.js',
  sourceCode: {
    parserServices: {
      esTreeNodeToTSNodeMap: new Map<TSESTree.Node, ts.Node>(),
      program: {},
      tsNodeToESTreeNodeMap: new Map<ts.Node, TSESTree.Node>(),
    } as unknown as ParserServices,
  },
} as unknown as UnknownRuleContext` | ✗ |


---

## Functions

### `createMockRuleContext(overrides: Partial<UnknownRuleContext>): UnknownRuleContext`

<details><summary>Code</summary>

```ts
(
  overrides: Partial<UnknownRuleContext> = {},
): UnknownRuleContext =>
  ({
    ...defaults,
    ...overrides,
  }) as unknown as UnknownRuleContext
```
</details>

- **Parameters**:
  - `overrides: Partial<UnknownRuleContext>`
- **Return Type**: `UnknownRuleContext`
### `requiresParserServicesMessageTemplate(parser: string): string`

<details><summary>Code</summary>

```ts
(parser = '\\S*'): string =>
  'You have used a rule which requires type information, .+\n' +
  `Parser: ${parser}`
```
</details>

- **Parameters**:
  - `parser: string`
- **Return Type**: `string`
### `baseErrorRegex(parser: string): RegExp`

<details><summary>Code</summary>

```ts
(parser?: string): RegExp =>
  new RegExp(requiresParserServicesMessageTemplate(parser))
```
</details>

- **Parameters**:
  - `parser: string`
- **Return Type**: `RegExp`
### `unknownParserErrorRegex(parser: string): RegExp`

<details><summary>Code</summary>

```ts
(parser?: string): RegExp =>
  new RegExp(
    `${requiresParserServicesMessageTemplate(parser)}
Note: detected a parser other than @typescript-eslint/parser. Make sure the parser is configured to forward "parserOptions.project" to @typescript-eslint/parser.`,
  )
```
</details>

- **Parameters**:
  - `parser: string`
- **Return Type**: `RegExp`

---

## Type Aliases

### `UnknownRuleContext`

```ts
type UnknownRuleContext = Readonly<TSESLint.RuleContext<string, unknown[]>>;
```


---