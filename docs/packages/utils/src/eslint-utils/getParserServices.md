[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getParserServices.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/utils/src/eslint-utils/getParserServices.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserServices` | `../ts-estree` |
| `ParserServicesWithTypeInformation` | `../ts-estree` |
| `parserSeemsToBeTSESLint` | `./parserSeemsToBeTSESLint` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---