[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `custom-matchers.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 28
- **Classes**: 0
- **Imports**: 13
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/tests/test-utils/custom-matchers/custom-matchers.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserOptions` | `@typescript-eslint/parser` |
| `ParserServices` | `@typescript-eslint/typescript-estree` |
| `ParserServicesWithTypeInformation` | `@typescript-eslint/typescript-estree` |
| `TSESTree` | `@typescript-eslint/typescript-estree` |
| `parseForESLint` | `@typescript-eslint/parser` |
| `Ajv` | `ajv` |
| `ReadonlynessOptions` | `../../../src/index.js` |
| `TypeOrValueSpecifier` | `../../../src/index.js` |
| `containsAllTypesByName` | `../../../src/index.js` |
| `isTypeReadonly` | `../../../src/index.js` |
| `isUnsafeAssignment` | `../../../src/index.js` |
| `typeMatchesSpecifier` | `../../../src/index.js` |
| `typeOrValueSpecifiersSchema` | `../../../src/index.js` |


---

## Functions

### `parserServices(this: Chai.AssertionStatic, errorMessage: string): void`

<details><summary>Code</summary>

```ts
function parserServices(this: Chai.AssertionStatic, errorMessage?: string) {
    if (errorMessage) {
      utils.flag(this, 'message', errorMessage);
    }

    const services: ParserServices | null | undefined = utils.flag(
      this,
      'object',
    );

    const negate: boolean = utils.flag(this, 'negate') ?? false;

    const ssfi: (...args: unknown[]) => unknown = utils.flag(this, 'ssfi');

    const assertion = new chai.Assertion(services, errorMessage, ssfi, true);

    if (negate) {
      (utils.hasProperty(services, 'program')
        ? assertion
        : assertion.not
      ).to.have
        .property('program')
        .that.equals(null);
    } else {
      assertion.to.have.property('program').that.does.not.equal(null);
    }
  }
```
</details>

- **Parameters**:
  - `this: Chai.AssertionStatic`
  - `errorMessage: string`
- **Return Type**: `void`
- **Calls**:
  - `utils.flag`
  - `(utils.hasProperty(services, 'program')
        ? assertion
        : assertion.not
      ).to.have
        .property('program')
        .that.equals`
  - `assertion.to.have.property('program').that.does.not.equal`
### `hasParserServicesWithTypeInformation(parseForESLintResult: T): asserts parseForESLintResult is T & {
  services: ParserServicesWithTypeInformation;
}`

<details><summary>Code</summary>

```ts
function hasParserServicesWithTypeInformation<
  T extends ReturnType<typeof parseForESLint>,
>(
  parseForESLintResult: T,
): asserts parseForESLintResult is T & {
  services: ParserServicesWithTypeInformation;
} {
  assert.isParserServices(parseForESLintResult.services);
}
```
</details>

- **Parameters**:
  - `parseForESLintResult: T`
- **Return Type**: `asserts parseForESLintResult is T & {
  services: ParserServicesWithTypeInformation;
}`
- **Calls**:
  - `assert.isParserServices`
### `parseCodeForEslint(code: string): ReturnType<
  typeof parseForESLint
> & {
  services: ParserServicesWithTypeInformation;
}`

<details><summary>Code</summary>

```ts
export function parseCodeForEslint(code: string): ReturnType<
  typeof parseForESLint
> & {
  services: ParserServicesWithTypeInformation;
} {
  const parseForESLintResult = parseForESLint(code, DEFAULT_PARSER_OPTIONS);

  hasParserServicesWithTypeInformation(parseForESLintResult);

  return parseForESLintResult;
}
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `ReturnType<
  typeof parseForESLint
> & {
  services: ParserServicesWithTypeInformation;
}`
- **Calls**:
  - `parseForESLint (from @typescript-eslint/parser)`
  - `hasParserServicesWithTypeInformation`
### `getTypes(code: string, declarationIndex: number): {
  checker: ts.TypeChecker;
  receiver: ts.Type;
  sender: ts.Type;
  senderNode: TSESTree.Node;
}`

<details><summary>Code</summary>

```ts
function getTypes(
  code: string,
  declarationIndex = 0,
): {
  checker: ts.TypeChecker;
  receiver: ts.Type;
  sender: ts.Type;
  senderNode: TSESTree.Node;
} {
  const { ast, services } = parseCodeForEslint(code);

  const checker = services.program.getTypeChecker();

  const declaration = ast.body[
    declarationIndex
  ] as TSESTree.VariableDeclaration;

  const declarator = declaration.declarations[0];

  assert.isNotNull(declarator.init);

  return {
    checker,
    receiver: services.getTypeAtLocation(declarator.id),
    sender: services.getTypeAtLocation(declarator.init),
    senderNode: declarator.init,
  };
}
```
</details>

- **Parameters**:
  - `code: string`
  - `declarationIndex: number`
- **Return Type**: `{
  checker: ts.TypeChecker;
  receiver: ts.Type;
  sender: ts.Type;
  senderNode: TSESTree.Node;
}`
- **Calls**:
  - `parseCodeForEslint`
  - `services.program.getTypeChecker`
  - `assert.isNotNull`
  - `services.getTypeAtLocation`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected type to${isNot ? ' not' : ''} be readonly:\n\n${printReceived(
          code,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected type to${isNot ? ' not' : ''} be readonly:\n\n${printReceived(
          code,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() => `Expected Assignment${isNot ? ' not' : ''} to be safe.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() => `Expected Assignment${isNot ? ' not' : ''} to be safe.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected specifier to${isNot ? ' not' : ''} be valid:\n\n${printReceived(
          typeOrValueSpecifier,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected specifier to${isNot ? ' not' : ''} be valid:\n\n${printReceived(
          typeOrValueSpecifier,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected type to${isNot ? ' not' : ''} contain all types by name:\n\n${printReceived(
          code,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected type to${isNot ? ' not' : ''} contain all types by name:\n\n${printReceived(
          code,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected types of sender and receiver to${isNot ? ' not' : ''} match.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected types of sender and receiver to${isNot ? ' not' : ''} match.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected type to${isNot ? ' not' : ''} match specifier:\n\n${printReceived(
          expectedTypeOrValueSpecifier,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected type to${isNot ? ' not' : ''} match specifier:\n\n${printReceived(
          expectedTypeOrValueSpecifier,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected type to${isNot ? ' not' : ''} be readonly:\n\n${printReceived(
          code,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected type to${isNot ? ' not' : ''} be readonly:\n\n${printReceived(
          code,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() => `Expected Assignment${isNot ? ' not' : ''} to be safe.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() => `Expected Assignment${isNot ? ' not' : ''} to be safe.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected specifier to${isNot ? ' not' : ''} be valid:\n\n${printReceived(
          typeOrValueSpecifier,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected specifier to${isNot ? ' not' : ''} be valid:\n\n${printReceived(
          typeOrValueSpecifier,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected type to${isNot ? ' not' : ''} contain all types by name:\n\n${printReceived(
          code,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected type to${isNot ? ' not' : ''} contain all types by name:\n\n${printReceived(
          code,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected types of sender and receiver to${isNot ? ' not' : ''} match.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected types of sender and receiver to${isNot ? ' not' : ''} match.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected type to${isNot ? ' not' : ''} match specifier:\n\n${printReceived(
          expectedTypeOrValueSpecifier,
        )}`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected type to${isNot ? ' not' : ''} match specifier:\n\n${printReceived(
          expectedTypeOrValueSpecifier,
        )}`
```
</details>

- **Return Type**: `string`

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