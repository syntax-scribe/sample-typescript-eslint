[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `custom-matchers.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/util/custom-matchers/custom-matchers.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserResponse` | `../parsers/parser-types.js` |
| `ParserResponseType` | `../parsers/parser-types.js` |


---

## Functions

### `successResponse(this: Chai.AssertionStatic, errorMessage: string): void`

<details><summary>Code</summary>

```ts
function successResponse(this: Chai.AssertionStatic, errorMessage?: string) {
    if (errorMessage) {
      utils.flag(this, 'message', errorMessage);
    }

    const thing: ParserResponse = utils.flag(this, 'object');

    const negate: boolean = utils.flag(this, 'negate') ?? false;

    const ssfi: (...args: unknown[]) => unknown = utils.flag(this, 'ssfi');

    const assertion = new chai.Assertion(thing, errorMessage, ssfi, true);

    if (negate) {
      (utils.hasProperty(thing, 'type') ? assertion : assertion.not).to.have
        .property('type')
        .that.does.not.equals(ParserResponseType.NoError);
    } else {
      assertion.to.have
        .property('type')
        .that.equals(ParserResponseType.NoError);
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
  - `(utils.hasProperty(thing, 'type') ? assertion : assertion.not).to.have
        .property('type')
        .that.does.not.equals`
  - `assertion.to.have
        .property('type')
        .that.equals`
### `errorResponse(this: Chai.AssertionStatic, errorMessage: string): void`

<details><summary>Code</summary>

```ts
function errorResponse(this: Chai.AssertionStatic, errorMessage?: string) {
    if (errorMessage) {
      utils.flag(this, 'message', errorMessage);
    }

    const thing: ParserResponse = utils.flag(this, 'object');

    const negate: boolean = utils.flag(this, 'negate') ?? false;

    const ssfi: (...args: unknown[]) => unknown = utils.flag(this, 'ssfi');

    const assertion = new chai.Assertion(thing, errorMessage, ssfi, true);

    if (negate) {
      (utils.hasProperty(thing, 'type') ? assertion : assertion.not).to.have
        .property('type')
        .that.does.not.equals(ParserResponseType.Error);
    } else {
      assertion.to.have.property('type').that.equals(ParserResponseType.Error);
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
  - `(utils.hasProperty(thing, 'type') ? assertion : assertion.not).to.have
        .property('type')
        .that.does.not.equals`
  - `assertion.to.have.property('type').that.equals`

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