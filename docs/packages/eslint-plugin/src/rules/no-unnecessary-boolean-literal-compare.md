[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-boolean-literal-compare.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 5 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unnecessary-boolean-literal-compare.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstraintInfo` | `../util` |
| `getParserServices` | `../util` |
| `isStrongPrecedenceNode` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `hasNonNullishType` | `boolean` | const | `nonNullishTypes.length > 0` | ✗ |
| `hasNullableType` | `boolean` | const | `nonNullishTypes.length < types.length` | ✗ |
| `negated` | `boolean` | const | `!comparisonType.isPositive` | ✗ |
| `shouldNegate` | `boolean` | let/var | `comparison.negated !== comparison.literalBooleanInComparison` | ✗ |
| `mutatedNode` | `any` | let/var | `isUnaryNegation ? node.parent : node` | ✗ |


---

## Functions

### `getBooleanComparison(node: TSESTree.BinaryExpression): BooleanComparisonWithTypeInformation | undefined`

<details><summary>Code</summary>

```ts
function getBooleanComparison(
      node: TSESTree.BinaryExpression,
    ): BooleanComparisonWithTypeInformation | undefined {
      const comparison = deconstructComparison(node);
      if (!comparison) {
        return undefined;
      }

      const { constraintType, isTypeParameter } = getConstraintInfo(
        checker,
        services.getTypeAtLocation(comparison.expression),
      );

      if (isTypeParameter && constraintType == null) {
        return undefined;
      }

      if (isBooleanType(constraintType)) {
        return {
          ...comparison,
          expressionIsNullableBoolean: false,
        };
      }

      if (isNullableBoolean(constraintType)) {
        return {
          ...comparison,
          expressionIsNullableBoolean: true,
        };
      }

      return undefined;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.BinaryExpression`
- **Return Type**: `BooleanComparisonWithTypeInformation | undefined`
- **Calls**:
  - `deconstructComparison`
  - `getConstraintInfo (from ../util)`
  - `services.getTypeAtLocation`
  - `isBooleanType`
  - `isNullableBoolean`
### `isBooleanType(expressionType: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isBooleanType(expressionType: ts.Type): boolean {
      return tsutils.isTypeFlagSet(
        expressionType,
        ts.TypeFlags.Boolean | ts.TypeFlags.BooleanLiteral,
      );
    }
```
</details>

- **Parameters**:
  - `expressionType: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.isTypeFlagSet`
### `isNullableBoolean(expressionType: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isNullableBoolean(expressionType: ts.Type): boolean {
      if (!expressionType.isUnion()) {
        return false;
      }

      const { types } = expressionType;

      const nonNullishTypes = types.filter(
        type =>
          !tsutils.isTypeFlagSet(
            type,
            ts.TypeFlags.Undefined | ts.TypeFlags.Null,
          ),
      );

      const hasNonNullishType = nonNullishTypes.length > 0;
      if (!hasNonNullishType) {
        return false;
      }

      const hasNullableType = nonNullishTypes.length < types.length;
      if (!hasNullableType) {
        return false;
      }

      const allNonNullishTypesAreBoolean = nonNullishTypes.every(isBooleanType);
      if (!allNonNullishTypesAreBoolean) {
        return false;
      }

      return true;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * checks if the expressionType is a union that
     *   1) contains at least one nullish type (null or undefined)
     *   2) contains at least once boolean type (true or false or boolean)
     *   3) does not contain any types besides nullish and boolean types
     */
```

- **Parameters**:
  - `expressionType: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `expressionType.isUnion`
  - `types.filter`
  - `tsutils.isTypeFlagSet`
  - `nonNullishTypes.every`
### `deconstructComparison(node: TSESTree.BinaryExpression): BooleanComparison | undefined`

<details><summary>Code</summary>

```ts
function deconstructComparison(
      node: TSESTree.BinaryExpression,
    ): BooleanComparison | undefined {
      const comparisonType = getEqualsKind(node.operator);
      if (!comparisonType) {
        return undefined;
      }

      for (const [against, expression] of [
        [node.right, node.left],
        [node.left, node.right],
      ]) {
        if (
          against.type !== AST_NODE_TYPES.Literal ||
          typeof against.value !== 'boolean'
        ) {
          continue;
        }

        const { value: literalBooleanInComparison } = against;
        const negated = !comparisonType.isPositive;

        return {
          expression,
          literalBooleanInComparison,
          negated,
        };
      }

      return undefined;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.BinaryExpression`
- **Return Type**: `BooleanComparison | undefined`
- **Calls**:
  - `getEqualsKind`
### `nodeIsUnaryNegation(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function nodeIsUnaryNegation(node: TSESTree.Node): boolean {
      return (
        node.type === AST_NODE_TYPES.UnaryExpression &&
        node.prefix &&
        node.operator === '!'
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `getEqualsKind(operator: string): EqualsKind | undefined`

<details><summary>Code</summary>

```ts
function getEqualsKind(operator: string): EqualsKind | undefined {
  switch (operator) {
    case '!=':
      return {
        isPositive: false,
        isStrict: false,
      };

    case '!==':
      return {
        isPositive: false,
        isStrict: true,
      };

    case '==':
      return {
        isPositive: true,
        isStrict: false,
      };

    case '===':
      return {
        isPositive: true,
        isStrict: true,
      };

    default:
      return undefined;
  }
}
```
</details>

- **Parameters**:
  - `operator: string`
- **Return Type**: `EqualsKind | undefined`

---

## Interfaces

### `BooleanComparison`

<details><summary>Interface Code</summary>

```ts
interface BooleanComparison {
  expression: TSESTree.Expression | TSESTree.PrivateIdentifier;
  literalBooleanInComparison: boolean;
  negated: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `expression` | `TSESTree.Expression | TSESTree.PrivateIdentifier` | ✗ |  |
| `literalBooleanInComparison` | `boolean` | ✗ |  |
| `negated` | `boolean` | ✗ |  |

### `BooleanComparisonWithTypeInformation`

<details><summary>Interface Code</summary>

```ts
interface BooleanComparisonWithTypeInformation extends BooleanComparison {
  expressionIsNullableBoolean: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `expressionIsNullableBoolean` | `boolean` | ✗ |  |

### `EqualsKind`

<details><summary>Interface Code</summary>

```ts
interface EqualsKind {
  isPositive: boolean;
  isStrict: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `isPositive` | `boolean` | ✗ |  |
| `isStrict` | `boolean` | ✗ |  |


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = | 'comparingNullableToFalse'
  | 'comparingNullableToTrueDirect'
  | 'comparingNullableToTrueNegated'
  | 'direct'
  | 'negated'
  | 'noStrictNullCheck';
```

### `Options`

```ts
type Options = [
  {
    allowComparingNullableBooleansToFalse?: boolean;
    allowComparingNullableBooleansToTrue?: boolean;
    allowRuleToRunWithoutStrictNullChecksIKnowWhatIAmDoing?: boolean;
  },
];
```


---