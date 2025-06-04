[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `custom-matchers.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 6 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/typescript-estree/tests/test-utils/custom-matchers/custom-matchers.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserServices` | `../../../src/index.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `negate` | `boolean` | const | `utils.flag(this, 'negate') ?? false` | ✗ |
| `assertion` | `Assertion` | const | `new chai.Assertion(services, errorMessage, ssfi, true)` | ✗ |
| `negate` | `boolean` | const | `utils.flag(this, 'negate') ?? false` | ✗ |
| `nodeTypeAssertion` | `Assertion` | const | `new chai.Assertion(
      nodeType,
      errorMessage,
      ssfi,
      true,
    )` | ✗ |
| `typeArgumentsAssertion` | `Assertion` | const | `new chai.Assertion(
      typeArguments,
      errorMessage,
      ssfi,
      true,
    )` | ✗ |
| `firstTypeArgumentAssertion` | `Assertion` | const | `new chai.Assertion(
      typeArguments[0],
      errorMessage,
      ssfi,
      true,
    )` | ✗ |


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
### `TSNodeOfNumberArrayType(this: Chai.AssertionStatic, errorMessage: string): void`

<details><summary>Code</summary>

```ts
function TSNodeOfNumberArrayType(
    this: Chai.AssertionStatic,
    errorMessage?: string,
  ) {
    if (errorMessage) {
      utils.flag(this, 'message', errorMessage);
    }

    const { checker, tsNode }: { checker: ts.TypeChecker; tsNode: ts.Node } =
      utils.flag(this, 'object');

    const ssfi: (...args: unknown[]) => unknown = utils.flag(this, 'ssfi');

    const negate: boolean = utils.flag(this, 'negate') ?? false;

    const nodeType = checker.getTypeAtLocation(tsNode);

    const typeArguments = checker.getTypeArguments(
      nodeType as ts.TypeReference,
    );

    const nodeTypeAssertion = new chai.Assertion(
      nodeType,
      errorMessage,
      ssfi,
      true,
    );

    const typeArgumentsAssertion = new chai.Assertion(
      typeArguments,
      errorMessage,
      ssfi,
      true,
    );

    const firstTypeArgumentAssertion = new chai.Assertion(
      typeArguments[0],
      errorMessage,
      ssfi,
      true,
    );

    if (negate) {
      (utils.hasProperty(nodeType, 'flags')
        ? nodeTypeAssertion
        : nodeTypeAssertion.not
      ).to.have
        .property('flags')
        .that.equals(ts.TypeFlags.Object);

      (utils.hasProperty(nodeType, 'objectFlags')
        ? nodeTypeAssertion
        : nodeTypeAssertion.not
      ).to.have
        .property('objectFlags')
        .that.equals(ts.ObjectFlags.Reference);

      typeArgumentsAssertion.not.lengthOf(1);

      (utils.hasProperty(firstTypeArgumentAssertion, 'flags')
        ? firstTypeArgumentAssertion
        : firstTypeArgumentAssertion.not
      ).to.have
        .property('flags')
        .that.does.not.equal(ts.TypeFlags.Number);
    } else {
      nodeTypeAssertion.to.have
        .property('flags')
        .that.equals(ts.TypeFlags.Object);

      nodeTypeAssertion.to.have
        .property('objectFlags')
        .that.equals(ts.ObjectFlags.Reference);

      typeArgumentsAssertion.lengthOf(1);

      firstTypeArgumentAssertion.to.have
        .property('flags')
        .that.equals(ts.TypeFlags.Number);
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
  - `checker.getTypeAtLocation`
  - `checker.getTypeArguments`
  - `(utils.hasProperty(nodeType, 'flags')
        ? nodeTypeAssertion
        : nodeTypeAssertion.not
      ).to.have
        .property('flags')
        .that.equals`
  - `(utils.hasProperty(nodeType, 'objectFlags')
        ? nodeTypeAssertion
        : nodeTypeAssertion.not
      ).to.have
        .property('objectFlags')
        .that.equals`
  - `typeArgumentsAssertion.not.lengthOf`
  - `(utils.hasProperty(firstTypeArgumentAssertion, 'flags')
        ? firstTypeArgumentAssertion
        : firstTypeArgumentAssertion.not
      ).to.have
        .property('flags')
        .that.does.not.equal`
  - `nodeTypeAssertion.to.have
        .property('flags')
        .that.equals`
  - `nodeTypeAssertion.to.have
        .property('objectFlags')
        .that.equals`
  - `typeArgumentsAssertion.lengthOf`
  - `firstTypeArgumentAssertion.to.have
        .property('flags')
        .that.equals`

---