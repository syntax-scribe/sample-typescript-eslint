[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getParserServices.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/utils/src/eslint-utils/getParserServices.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserServices` | `../ts-estree` |
| `ParserServicesWithTypeInformation` | `../ts-estree` |
| `parserSeemsToBeTSESLint` | `./parserSeemsToBeTSESLint` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ERROR_MESSAGE_REQUIRES_PARSER_SERVICES` | `"You have used a rule which requires type information, but don't have parserOptions set to generate type information for this file. See https://typescript-eslint.io/getting-started/typed-linting for enabling linting with type information."` | const | `"You have used a rule which requires type information, but don't have parserOptions set to generate type information for this file. See https://typescript-eslint.io/getting-started/typed-linting for enabling linting with type information."` | ✗ |
| `ERROR_MESSAGE_UNKNOWN_PARSER` | `"Note: detected a parser other than @typescript-eslint/parser. Make sure the parser is configured to forward \"parserOptions.project\" to @typescript-eslint/parser."` | const | `'Note: detected a parser other than @typescript-eslint/parser. Make sure the parser is configured to forward "parserOptions.project" to @typescript-eslint/parser.'` | ✗ |
| `parser` | `string` | const | `context.parserPath || context.languageOptions.parser?.meta?.name` | ✗ |


---

## Functions

### `getParserServices(context: Readonly<TSESLint.RuleContext<MessageIds, Options>>): ParserServicesWithTypeInformation`

<details><summary>Code</summary>

```ts
export function getParserServices<
  MessageIds extends string,
  Options extends readonly unknown[],
>(
  context: Readonly<TSESLint.RuleContext<MessageIds, Options>>,
): ParserServicesWithTypeInformation;
```
</details>

- **JSDoc**:
```ts
/**
 * Try to retrieve type-aware parser service from context.
 * This **_will_** throw if it is not available.
 */
```

- **Parameters**:
  - `context: Readonly<TSESLint.RuleContext<MessageIds, Options>>`
- **Return Type**: `ParserServicesWithTypeInformation`
### `throwError(parser: string | undefined): never`

<details><summary>Code</summary>

```ts
function throwError(parser: string | undefined): never {
  const messages = [
    ERROR_MESSAGE_REQUIRES_PARSER_SERVICES,
    `Parser: ${parser || '(unknown)'}`,
    !parserSeemsToBeTSESLint(parser) && ERROR_MESSAGE_UNKNOWN_PARSER,
  ].filter(Boolean);

  throw new Error(messages.join('\n'));
}
```
</details>

- **Parameters**:
  - `parser: string | undefined`
- **Return Type**: `never`
- **Calls**:
  - `[
    ERROR_MESSAGE_REQUIRES_PARSER_SERVICES,
    `Parser: ${parser || '(unknown)'}`,
    !parserSeemsToBeTSESLint(parser) && ERROR_MESSAGE_UNKNOWN_PARSER,
  ].filter`
  - `parserSeemsToBeTSESLint (from ./parserSeemsToBeTSESLint)`
  - `messages.join`

---