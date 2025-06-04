[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `custom-matchers.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/util/custom-matchers/custom-matchers.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserResponse` | `../parsers/parser-types.js` |
| `ParserResponseType` | `../parsers/parser-types.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `negate` | `boolean` | const | `utils.flag(this, 'negate') ?? false` | ✗ |
| `assertion` | `Assertion` | const | `new chai.Assertion(thing, errorMessage, ssfi, true)` | ✗ |
| `negate` | `boolean` | const | `utils.flag(this, 'negate') ?? false` | ✗ |
| `assertion` | `Assertion` | const | `new chai.Assertion(thing, errorMessage, ssfi, true)` | ✗ |


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