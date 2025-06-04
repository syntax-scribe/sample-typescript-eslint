[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `non-nullable-type-assertion-style.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/non-nullable-type-assertion-style.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getOperatorPrecedence` | `../util` |
| `getParserServices` | `../util` |
| `OperatorPrecedence` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `higherPrecedenceThanUnary` | `boolean` | const | `getOperatorPrecedence(
              services.esTreeNodeToTSNodeMap.get(node.expression).kind,
              ts.SyntaxKind.Unknown,
            ) > OperatorPrecedence.Unary` | ✗ |


---

## Functions

### `getTypesIfNotLoose(node: TSESTree.Node): ts.Type[] | undefined`

<details><summary>Code</summary>

```ts
(node: TSESTree.Node): ts.Type[] | undefined => {
      const type = services.getTypeAtLocation(node);

      if (
        tsutils.isTypeFlagSet(type, ts.TypeFlags.Any | ts.TypeFlags.Unknown)
      ) {
        return undefined;
      }

      return tsutils.unionConstituents(type);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `ts.Type[] | undefined`
- **Calls**:
  - `services.getTypeAtLocation`
  - `tsutils.isTypeFlagSet`
  - `tsutils.unionConstituents`
### `couldBeNullish(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
(type: ts.Type): boolean => {
      if (type.flags & ts.TypeFlags.TypeParameter) {
        const constraint = type.getConstraint();
        return constraint == null || couldBeNullish(constraint);
      }

      if (tsutils.isUnionType(type)) {
        for (const part of type.types) {
          if (couldBeNullish(part)) {
            return true;
          }
        }
        return false;
      }
      return (type.flags & (ts.TypeFlags.Null | ts.TypeFlags.Undefined)) !== 0;
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `type.getConstraint`
  - `couldBeNullish`
  - `tsutils.isUnionType`
### `sameTypeWithoutNullish(assertedTypes: ts.Type[], originalTypes: ts.Type[]): boolean`

<details><summary>Code</summary>

```ts
(
      assertedTypes: ts.Type[],
      originalTypes: ts.Type[],
    ): boolean => {
      const nonNullishOriginalTypes = originalTypes.filter(
        type =>
          (type.flags & (ts.TypeFlags.Null | ts.TypeFlags.Undefined)) === 0,
      );

      if (nonNullishOriginalTypes.length === originalTypes.length) {
        return false;
      }

      for (const assertedType of assertedTypes) {
        if (
          couldBeNullish(assertedType) ||
          !nonNullishOriginalTypes.includes(assertedType)
        ) {
          return false;
        }
      }

      for (const originalType of nonNullishOriginalTypes) {
        if (!assertedTypes.includes(originalType)) {
          return false;
        }
      }

      return true;
    }
```
</details>

- **Parameters**:
  - `assertedTypes: ts.Type[]`
  - `originalTypes: ts.Type[]`
- **Return Type**: `boolean`
- **Calls**:
  - `originalTypes.filter`
  - `couldBeNullish`
  - `nonNullishOriginalTypes.includes`
  - `assertedTypes.includes`
### `isConstAssertion(node: TSESTree.TSAsExpression | TSESTree.TSTypeAssertion): boolean`

<details><summary>Code</summary>

```ts
(
      node: TSESTree.TSAsExpression | TSESTree.TSTypeAssertion,
    ): boolean => {
      return (
        node.typeAnnotation.type === AST_NODE_TYPES.TSTypeReference &&
        node.typeAnnotation.typeName.type === AST_NODE_TYPES.Identifier &&
        node.typeAnnotation.typeName.name === 'const'
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSAsExpression | TSESTree.TSTypeAssertion`
- **Return Type**: `boolean`

---