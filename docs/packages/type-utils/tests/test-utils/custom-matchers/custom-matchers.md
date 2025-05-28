[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `custom-matchers.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 28 |
| 🧱 Classes | 0 |
| 📦 Imports | 13 |
| 📊 Variables & Constants | 15 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `DEFAULT_PARSER_OPTIONS` | `ParserOptions` | const | `{
  disallowAutomaticSingleRunInference: true,
  filePath: path.join(FIXTURES_DIR, 'file.ts'),
  project: './tsconfig.json',
  tsconfigRootDir: FIXTURES_DIR,
} satisfies ParserOptions` | ✗ |
| `negate` | `boolean` | const | `utils.flag(this, 'negate') ?? false` | ✗ |
| `assertion` | `Assertion` | const | `new chai.Assertion(services, errorMessage, ssfi, true)` | ✗ |
| `declaration` | `TSESTree.VariableDeclaration` | const | `ast.body[
    declarationIndex
  ] as TSESTree.VariableDeclaration` | ✗ |
| `declarator` | `any` | const | `declaration.declarations[0]` | ✗ |
| `declaration` | `TSESTree.TSTypeAliasDeclaration` | const | `ast.body[0] as TSESTree.TSTypeAliasDeclaration` | ✗ |
| `expected` | `false` | const | `false` | ✗ |
| `pass` | `boolean` | const | `actual === expected` | ✗ |
| `ajv` | `any` | const | `new Ajv()` | ✗ |
| `expected` | `true` | const | `true` | ✗ |
| `pass` | `boolean` | const | `actual === expected` | ✗ |
| `declaration` | `TSESTree.TSTypeAliasDeclaration` | const | `ast.body[0] as TSESTree.TSTypeAliasDeclaration` | ✗ |
| `actual` | `{ receiver: any; sender: any; }` | const | `{ receiver: receiverType, sender: senderType }` | ✗ |
| `expected` | `{ receiver: string; sender: string; }` | const | `{ receiver: receiverStr, sender: senderStr }` | ✗ |
| `pass` | `boolean` | const | `receiverType === receiverStr && senderType === senderStr` | ✗ |


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