[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `custom-matchers.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 45
- **Classes**: 0
- **Imports**: 10
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/test-utils/custom-matchers/custom-matchers.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `TSESTree` | `@typescript-eslint/types` |
| `TSESTreeOptions` | `@typescript-eslint/typescript-estree` |
| `parse` | `@typescript-eslint/typescript-estree` |
| `simpleTraverse` | `@typescript-eslint/typescript-estree` |
| `Definition` | `../../../src/index.js` |
| `DefinitionType` | `../../../src/index.js` |
| `Scope` | `../../../src/index.js` |
| `ScopeType` | `../../../src/index.js` |
| `analyze` | `../../../src/index.js` |


---

## Functions

### `scopeOfType(this: Chai.AssertionStatic, expectedScopeType: ScopeType, errorMessage: string): void`

<details><summary>Code</summary>

```ts
function scopeOfType(
    this: Chai.AssertionStatic,
    expectedScopeType: ScopeType,
    errorMessage?: string,
  ) {
    if (errorMessage) {
      utils.flag(this, 'message', errorMessage);
    }

    const scope: Scope | undefined = utils.flag(this, 'object');

    const negate: boolean = utils.flag(this, 'negate') ?? false;

    const ssfi: (...args: unknown[]) => unknown = utils.flag(this, 'ssfi');

    const assertion = new chai.Assertion(scope, errorMessage, ssfi, true);

    if (negate) {
      (utils.hasProperty(scope, 'type') ? assertion : assertion.not).to.have
        .property('type')
        .that.does.not.equal(expectedScopeType);
    } else {
      assertion.to.have.property('type').that.equals(expectedScopeType);
    }
  }
```
</details>

- **Parameters**:
  - `this: Chai.AssertionStatic`
  - `expectedScopeType: ScopeType`
  - `errorMessage: string`
- **Return Type**: `void`
- **Calls**:
  - `utils.flag`
  - `(utils.hasProperty(scope, 'type') ? assertion : assertion.not).to.have
        .property('type')
        .that.does.not.equal`
  - `assertion.to.have.property('type').that.equals`
### `definitionOfType(this: Chai.AssertionStatic, expectedDefinitionType: DefinitionType, errorMessage: string): void`

<details><summary>Code</summary>

```ts
function definitionOfType(
    this: Chai.AssertionStatic,
    expectedDefinitionType: DefinitionType,
    errorMessage?: string,
  ) {
    if (errorMessage) {
      utils.flag(this, 'message', errorMessage);
    }

    const definition: Definition | undefined = utils.flag(this, 'object');

    const negate: boolean = utils.flag(this, 'negate') ?? false;

    const ssfi: (...args: unknown[]) => unknown = utils.flag(this, 'ssfi');

    const assertion = new chai.Assertion(definition, errorMessage, ssfi, true);

    if (negate) {
      (utils.hasProperty(definition, 'type')
        ? assertion
        : assertion.not
      ).to.have
        .property('type')
        .that.does.not.equal(expectedDefinitionType);
    } else {
      assertion.to.have.property('type').that.equals(expectedDefinitionType);
    }
  }
```
</details>

- **Parameters**:
  - `this: Chai.AssertionStatic`
  - `expectedDefinitionType: DefinitionType`
  - `errorMessage: string`
- **Return Type**: `void`
- **Calls**:
  - `utils.flag`
  - `(utils.hasProperty(definition, 'type')
        ? assertion
        : assertion.not
      ).to.have
        .property('type')
        .that.does.not.equal`
  - `assertion.to.have.property('type').that.equals`
### `nodeOfType(this: Chai.AssertionStatic, expectedNodeType: AST_NODE_TYPES, errorMessage: string): void`

<details><summary>Code</summary>

```ts
function nodeOfType(
    this: Chai.AssertionStatic,
    expectedNodeType: AST_NODE_TYPES,
    errorMessage?: string,
  ) {
    if (errorMessage) {
      utils.flag(this, 'message', errorMessage);
    }

    const node: TSESTree.Node | null | undefined = utils.flag(this, 'object');

    const negate: boolean = utils.flag(this, 'negate') ?? false;

    const ssfi: (...args: unknown[]) => unknown = utils.flag(this, 'ssfi');

    const assertion = new chai.Assertion(node, errorMessage, ssfi, true);

    if (negate) {
      (utils.hasProperty(node, 'type') ? assertion : assertion.not).to.have
        .property('type')
        .that.does.not.equal(expectedNodeType);
    } else {
      assertion.to.have.property('type').that.equals(expectedNodeType);
    }
  }
```
</details>

- **Parameters**:
  - `this: Chai.AssertionStatic`
  - `expectedNodeType: AST_NODE_TYPES`
  - `errorMessage: string`
- **Return Type**: `void`
- **Calls**:
  - `utils.flag`
  - `(utils.hasProperty(node, 'type') ? assertion : assertion.not).to.have
        .property('type')
        .that.does.not.equal`
  - `assertion.to.have.property('type').that.equals`
### `message(): string`

<details><summary>Code</summary>

```ts
() => ``
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() => ``
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() => ``
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected the name list array${isNot ? ' not' : ''} to be empty.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected the name list array${isNot ? ' not' : ''} to be empty.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() => ``
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() => ``
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() => ``
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                `Expected both arrays${isNot ? ' not' : ''} to have the same length.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
                  `Expected both arrays${isNot ? ' not' : ''} to be equal.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected the name list array${isNot ? ' not' : ''} to be empty.`
```
</details>

- **Return Type**: `string`
### `message(): string`

<details><summary>Code</summary>

```ts
() =>
        `Expected the name list array${isNot ? ' not' : ''} to be empty.`
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