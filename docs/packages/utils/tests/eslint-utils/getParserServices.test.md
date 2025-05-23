[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getParserServices.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 4
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 1

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `UnknownRuleContext`

```ts
type UnknownRuleContext = Readonly<TSESLint.RuleContext<string, unknown[]>>;
```


---