[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-condition.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 37 |
| 📦 Imports | 22 |
| 📊 Variables & Constants | 18 |
| 📑 Type Aliases | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unnecessary-condition.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getConstraintInfo` | `../util` |
| `getParserServices` | `../util` |
| `getTypeName` | `../util` |
| `getTypeOfPropertyOfName` | `../util` |
| `getValueOfLiteralType` | `../util` |
| `isArrayMethodCallWithPredicate` | `../util` |
| `isIdentifier` | `../util` |
| `isNullableType` | `../util` |
| `isPossiblyFalsy` | `../util` |
| `isPossiblyTruthy` | `../util` |
| `isTypeAnyType` | `../util` |
| `isTypeFlagSet` | `../util` |
| `isTypeUnknownType` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |
| `findTruthinessAssertedArgument` | `../util/assertionFunctionUtils` |
| `findTypeGuardAssertedArgument` | `../util/assertionFunctionUtils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `nullishFlag` | `number` | const | `ts.TypeFlags.Undefined | ts.TypeFlags.Null` | ✗ |
| `BOOL_OPERATORS` | `Set<"==" | "===" | "<" | ">" | "<=" | ">=" | "!=" | "!==">` | const | `new Set([
  '<',
  '>',
  '<=',
  '>=',
  '==',
  '===',
  '!=',
  '!==',
] as const)` | ✗ |
| `constantLoopConditionsAllowedLiterals` | `Set<unknown>` | const | `new Set<unknown>([
  true,
  false,
  1,
  0,
])` | ✗ |
| `property` | `any` | const | `node.property` | ✗ |
| `messageId` | `MessageId | null` | let/var | `null` | ✗ |
| `messageId` | `MessageId | null` | let/var | `null` | ✗ |
| `UNDEFINED` | `any` | const | `ts.TypeFlags.Undefined` | ✗ |
| `NULL` | `any` | const | `ts.TypeFlags.Null` | ✗ |
| `VOID` | `any` | const | `ts.TypeFlags.Void` | ✗ |
| `callback` | `any` | const | `node.arguments[0]` | ✗ |
| `callbackBody` | `any` | const | `callback.body.body` | ✗ |
| `hasFalsyReturnTypes` | `boolean` | let/var | `false` | ✗ |
| `hasTruthyReturnTypes` | `boolean` | let/var | `false` | ✗ |
| `lhsNode` | `any` | const | `node.type === AST_NODE_TYPES.CallExpression ? node.callee : node.object` | ✗ |
| `property` | `any` | const | `node.property` | ✗ |
| `isStringTypeName` | `boolean` | const | `getTypeName(checker, info.keyType) === 'string'` | ✗ |
| `isOwnNullable` | `boolean` | const | `node.type === AST_NODE_TYPES.MemberExpression
          ? !isMemberExpressionNullableOriginFromObject(node)
          : node.type === AST_NODE_TYPES.CallExpression
            ? !isCallExpressionNullableOriginFromCallee(node)
            : true` | ✗ |
| `nodeToCheck` | `any` | const | `node.type === AST_NODE_TYPES.CallExpression ? node.callee : node.object` | ✗ |


---

## Functions

### `isNullishType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isNullishType(type: ts.Type): boolean {
  return tsutils.isTypeFlagSet(type, nullishFlag);
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.isTypeFlagSet`
### `isAlwaysNullish(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isAlwaysNullish(type: ts.Type): boolean {
  return tsutils.unionConstituents(type).every(isNullishType);
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.unionConstituents(type).every`
### `isPossiblyNullish(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isPossiblyNullish(type: ts.Type): boolean {
  return tsutils.unionConstituents(type).some(isNullishType);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Note that this differs from {@link isNullableType} in that it doesn't consider
 * `any` or `unknown` to be nullable.
 */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.unionConstituents(type).some`
### `toStaticValue(type: ts.Type): | { value: bigint | boolean | number | string | null | undefined }
  | undefined`

<details><summary>Code</summary>

```ts
function toStaticValue(
  type: ts.Type,
):
  | { value: bigint | boolean | number | string | null | undefined }
  | undefined {
  // type.isLiteral() only covers numbers/bigints and strings, hence the rest of the branches.
  if (tsutils.isBooleanLiteralType(type)) {
    return { value: tsutils.isTrueLiteralType(type) };
  }
  if (type.flags === ts.TypeFlags.Undefined) {
    return { value: undefined };
  }
  if (type.flags === ts.TypeFlags.Null) {
    return { value: null };
  }
  if (type.isLiteral()) {
    return { value: getValueOfLiteralType(type) };
  }

  return undefined;
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `| { value: bigint | boolean | number | string | null | undefined }
  | undefined`
- **Calls**:
  - `tsutils.isBooleanLiteralType`
  - `tsutils.isTrueLiteralType`
  - `type.isLiteral`
  - `getValueOfLiteralType (from ../util)`
- **Internal Comments**:
```
// type.isLiteral() only covers numbers/bigints and strings, hence the rest of the branches.
```

### `isBoolOperator(operator: string): operator is BoolOperator`

<details><summary>Code</summary>

```ts
function isBoolOperator(operator: string): operator is BoolOperator {
  return (BOOL_OPERATORS as Set<string>).has(operator);
}
```
</details>

- **Parameters**:
  - `operator: string`
- **Return Type**: `operator is BoolOperator`
- **Calls**:
  - `(BOOL_OPERATORS as Set<string>).has`
### `booleanComparison(left: unknown, operator: BoolOperator, right: unknown): boolean`

<details><summary>Code</summary>

```ts
function booleanComparison(
  left: unknown,
  operator: BoolOperator,
  right: unknown,
): boolean {
  switch (operator) {
    case '!=':
      // eslint-disable-next-line eqeqeq -- intentionally comparing with loose equality
      return left != right;
    case '!==':
      return left !== right;
    case '<':
      // @ts-expect-error: we don't care if the comparison seems unintentional.
      return left < right;
    case '<=':
      // @ts-expect-error: we don't care if the comparison seems unintentional.
      return left <= right;
    case '==':
      // eslint-disable-next-line eqeqeq -- intentionally comparing with loose equality
      return left == right;
    case '===':
      return left === right;
    case '>':
      // @ts-expect-error: we don't care if the comparison seems unintentional.
      return left > right;
    case '>=':
      // @ts-expect-error: we don't care if the comparison seems unintentional.
      return left >= right;
  }
}
```
</details>

- **Parameters**:
  - `left: unknown`
  - `operator: BoolOperator`
  - `right: unknown`
- **Return Type**: `boolean`
- **Internal Comments**:
```
// eslint-disable-next-line eqeqeq -- intentionally comparing with loose equality (x2)
// @ts-expect-error: we don't care if the comparison seems unintentional. (x4)
```

### `nodeIsArrayType(node: TSESTree.Expression): boolean`

<details><summary>Code</summary>

```ts
function nodeIsArrayType(node: TSESTree.Expression): boolean {
      const nodeType = getConstrainedTypeAtLocation(services, node);
      return tsutils
        .unionConstituents(nodeType)
        .some(part => checker.isArrayType(part));
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `boolean`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `tsutils
        .unionConstituents(nodeType)
        .some`
  - `checker.isArrayType`
### `nodeIsTupleType(node: TSESTree.Expression): boolean`

<details><summary>Code</summary>

```ts
function nodeIsTupleType(node: TSESTree.Expression): boolean {
      const nodeType = getConstrainedTypeAtLocation(services, node);
      return tsutils
        .unionConstituents(nodeType)
        .some(part => checker.isTupleType(part));
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `boolean`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `tsutils
        .unionConstituents(nodeType)
        .some`
  - `checker.isTupleType`
### `isArrayIndexExpression(node: TSESTree.Expression): boolean`

<details><summary>Code</summary>

```ts
function isArrayIndexExpression(node: TSESTree.Expression): boolean {
      return (
        // Is an index signature
        node.type === AST_NODE_TYPES.MemberExpression &&
        node.computed &&
        // ...into an array type
        (nodeIsArrayType(node.object) ||
          // ... or a tuple type
          (nodeIsTupleType(node.object) &&
            // Exception: literal index into a tuple - will have a sound type
            node.property.type !== AST_NODE_TYPES.Literal))
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `boolean`
- **Calls**:
  - `nodeIsArrayType`
  - `nodeIsTupleType`
- **Internal Comments**:
```
// Is an index signature (x5)
// ...into an array type
// ... or a tuple type
// Exception: literal index into a tuple - will have a sound type (x4)
```

### `isConditionalAlwaysNecessary(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isConditionalAlwaysNecessary(type: ts.Type): boolean {
      return tsutils
        .unionConstituents(type)
        .some(
          part =>
            isTypeAnyType(part) ||
            isTypeUnknownType(part) ||
            isTypeFlagSet(part, ts.TypeFlags.TypeVariable),
        );
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils
        .unionConstituents(type)
        .some`
  - `isTypeAnyType (from ../util)`
  - `isTypeUnknownType (from ../util)`
  - `isTypeFlagSet (from ../util)`
### `isNullableMemberExpression(node: TSESTree.MemberExpression): boolean`

<details><summary>Code</summary>

```ts
function isNullableMemberExpression(
      node: TSESTree.MemberExpression,
    ): boolean {
      const objectType = services.getTypeAtLocation(node.object);
      if (node.computed) {
        const propertyType = services.getTypeAtLocation(node.property);
        return isNullablePropertyType(objectType, propertyType);
      }
      const property = node.property;

      // Get the actual property name, to account for private properties (this.#prop).
      const propertyName = context.sourceCode.getText(property);

      const propertyType = objectType
        .getProperties()
        .find(prop => prop.name === propertyName);

      if (
        propertyType &&
        tsutils.isSymbolFlagSet(propertyType, ts.SymbolFlags.Optional)
      ) {
        return true;
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.MemberExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `services.getTypeAtLocation`
  - `isNullablePropertyType`
  - `context.sourceCode.getText`
  - `objectType
        .getProperties()
        .find`
  - `tsutils.isSymbolFlagSet`
- **Internal Comments**:
```
// Get the actual property name, to account for private properties (this.#prop). (x2)
```

### `checkNode(expression: TSESTree.Expression, isUnaryNotArgument: boolean, node: TSESTree.Expression): void`

<details><summary>Code</summary>

```ts
function checkNode(
      expression: TSESTree.Expression,
      isUnaryNotArgument = false,
      node = expression,
    ): void {
      // Check if the node is Unary Negation expression and handle it
      if (
        expression.type === AST_NODE_TYPES.UnaryExpression &&
        expression.operator === '!'
      ) {
        return checkNode(expression.argument, !isUnaryNotArgument, node);
      }

      // Since typescript array index signature types don't represent the
      //  possibility of out-of-bounds access, if we're indexing into an array
      //  just skip the check, to avoid false positives
      if (!isNoUncheckedIndexedAccess && isArrayIndexExpression(expression)) {
        return;
      }

      // When checking logical expressions, only check the right side
      //  as the left side has been checked by checkLogicalExpressionForUnnecessaryConditionals
      //
      // Unless the node is nullish coalescing, as it's common to use patterns like `nullBool ?? true` to to strict
      //  boolean checks if we inspect the right here, it'll usually be a constant condition on purpose.
      // In this case it's better to inspect the type of the expression as a whole.
      if (
        expression.type === AST_NODE_TYPES.LogicalExpression &&
        expression.operator !== '??'
      ) {
        return checkNode(expression.right);
      }

      const type = getConstrainedTypeAtLocation(services, expression);

      if (isConditionalAlwaysNecessary(type)) {
        return;
      }
      let messageId: MessageId | null = null;

      if (isTypeFlagSet(type, ts.TypeFlags.Never)) {
        messageId = 'never';
      } else if (!isPossiblyTruthy(type)) {
        messageId = !isUnaryNotArgument ? 'alwaysFalsy' : 'alwaysTruthy';
      } else if (!isPossiblyFalsy(type)) {
        messageId = !isUnaryNotArgument ? 'alwaysTruthy' : 'alwaysFalsy';
      }

      if (messageId) {
        context.report({ node, messageId });
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if a conditional node is necessary:
     * if the type of the node is always true or always false, it's not necessary.
     */
```

- **Parameters**:
  - `expression: TSESTree.Expression`
  - `isUnaryNotArgument: boolean`
  - `node: TSESTree.Expression`
- **Return Type**: `void`
- **Calls**:
  - `checkNode`
  - `isArrayIndexExpression`
  - `getConstrainedTypeAtLocation (from ../util)`
  - `isConditionalAlwaysNecessary`
  - `isTypeFlagSet (from ../util)`
  - `isPossiblyTruthy (from ../util)`
  - `isPossiblyFalsy (from ../util)`
  - `context.report`
- **Internal Comments**:
```
// Check if the node is Unary Negation expression and handle it
// Since typescript array index signature types don't represent the
//  possibility of out-of-bounds access, if we're indexing into an array
//  just skip the check, to avoid false positives
// When checking logical expressions, only check the right side
//  as the left side has been checked by checkLogicalExpressionForUnnecessaryConditionals
//
// Unless the node is nullish coalescing, as it's common to use patterns like `nullBool ?? true` to to strict
//  boolean checks if we inspect the right here, it'll usually be a constant condition on purpose.
// In this case it's better to inspect the type of the expression as a whole.
```

### `checkNodeForNullish(node: TSESTree.Expression): void`

<details><summary>Code</summary>

```ts
function checkNodeForNullish(node: TSESTree.Expression): void {
      const type = getConstrainedTypeAtLocation(services, node);

      // Conditional is always necessary if it involves `any`, `unknown` or a naked type parameter
      if (
        isTypeFlagSet(
          type,
          ts.TypeFlags.Any |
            ts.TypeFlags.Unknown |
            ts.TypeFlags.TypeParameter |
            ts.TypeFlags.TypeVariable,
        )
      ) {
        return;
      }

      let messageId: MessageId | null = null;
      if (isTypeFlagSet(type, ts.TypeFlags.Never)) {
        messageId = 'never';
      } else if (
        !isPossiblyNullish(type) &&
        !(
          node.type === AST_NODE_TYPES.MemberExpression &&
          isNullableMemberExpression(node)
        )
      ) {
        // Since typescript array index signature types don't represent the
        //  possibility of out-of-bounds access, if we're indexing into an array
        //  just skip the check, to avoid false positives
        if (
          isNoUncheckedIndexedAccess ||
          (!isArrayIndexExpression(node) &&
            !(
              node.type === AST_NODE_TYPES.ChainExpression &&
              node.expression.type !== AST_NODE_TYPES.TSNonNullExpression &&
              optionChainContainsOptionArrayIndex(node.expression)
            ))
        ) {
          messageId = 'neverNullish';
        }
      } else if (isAlwaysNullish(type)) {
        messageId = 'alwaysNullish';
      }

      if (messageId) {
        context.report({ node, messageId });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `void`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `isTypeFlagSet (from ../util)`
  - `isPossiblyNullish`
  - `isNullableMemberExpression`
  - `isArrayIndexExpression`
  - `optionChainContainsOptionArrayIndex`
  - `isAlwaysNullish`
  - `context.report`
- **Internal Comments**:
```
// Conditional is always necessary if it involves `any`, `unknown` or a naked type parameter
// Since typescript array index signature types don't represent the
//  possibility of out-of-bounds access, if we're indexing into an array
//  just skip the check, to avoid false positives
```

### `checkIfBoolExpressionIsNecessaryConditional(node: TSESTree.Node, left: TSESTree.Node, right: TSESTree.Node, operator: BoolOperator): void`

<details><summary>Code</summary>

```ts
function checkIfBoolExpressionIsNecessaryConditional(
      node: TSESTree.Node,
      left: TSESTree.Node,
      right: TSESTree.Node,
      operator: BoolOperator,
    ): void {
      const leftType = getConstrainedTypeAtLocation(services, left);
      const rightType = getConstrainedTypeAtLocation(services, right);

      const leftStaticValue = toStaticValue(leftType);
      const rightStaticValue = toStaticValue(rightType);

      if (leftStaticValue != null && rightStaticValue != null) {
        const conditionIsTrue = booleanComparison(
          leftStaticValue.value,
          operator,
          rightStaticValue.value,
        );

        context.report({
          node,
          messageId: 'comparisonBetweenLiteralTypes',
          data: {
            left: checker.typeToString(leftType),
            operator,
            right: checker.typeToString(rightType),
            trueOrFalse: conditionIsTrue ? 'true' : 'false',
          },
        });
        return;
      }

      // Workaround for https://github.com/microsoft/TypeScript/issues/37160
      if (isStrictNullChecks) {
        const UNDEFINED = ts.TypeFlags.Undefined;
        const NULL = ts.TypeFlags.Null;
        const VOID = ts.TypeFlags.Void;
        const isComparable = (type: ts.Type, flag: ts.TypeFlags): boolean => {
          // Allow comparison to `any`, `unknown` or a naked type parameter.
          flag |=
            ts.TypeFlags.Any |
            ts.TypeFlags.Unknown |
            ts.TypeFlags.TypeParameter |
            ts.TypeFlags.TypeVariable;

          // Allow loose comparison to nullish values.
          if (operator === '==' || operator === '!=') {
            flag |= NULL | UNDEFINED | VOID;
          }

          return isTypeFlagSet(type, flag);
        };

        if (
          (leftType.flags === UNDEFINED &&
            !isComparable(rightType, UNDEFINED | VOID)) ||
          (rightType.flags === UNDEFINED &&
            !isComparable(leftType, UNDEFINED | VOID)) ||
          (leftType.flags === NULL && !isComparable(rightType, NULL)) ||
          (rightType.flags === NULL && !isComparable(leftType, NULL))
        ) {
          context.report({ node, messageId: 'noOverlapBooleanExpression' });
          return;
        }
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks that a binary expression is necessarily conditional, reports otherwise.
     * If both sides of the binary expression are literal values, it's not a necessary condition.
     *
     * NOTE: It's also unnecessary if the types that don't overlap at all
     *    but that case is handled by the Typescript compiler itself.
     *    Known exceptions:
     *      - https://github.com/microsoft/TypeScript/issues/32627
     *      - https://github.com/microsoft/TypeScript/issues/37160 (handled)
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `left: TSESTree.Node`
  - `right: TSESTree.Node`
  - `operator: BoolOperator`
- **Return Type**: `void`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `toStaticValue`
  - `booleanComparison`
  - `context.report`
  - `checker.typeToString`
  - `isTypeFlagSet (from ../util)`
  - `isComparable`
- **Internal Comments**:
```
// Workaround for https://github.com/microsoft/TypeScript/issues/37160
// Allow comparison to `any`, `unknown` or a naked type parameter. (x3)
// Allow loose comparison to nullish values.
```

### `isComparable(type: ts.Type, flag: ts.TypeFlags): boolean`

<details><summary>Code</summary>

```ts
(type: ts.Type, flag: ts.TypeFlags): boolean => {
          // Allow comparison to `any`, `unknown` or a naked type parameter.
          flag |=
            ts.TypeFlags.Any |
            ts.TypeFlags.Unknown |
            ts.TypeFlags.TypeParameter |
            ts.TypeFlags.TypeVariable;

          // Allow loose comparison to nullish values.
          if (operator === '==' || operator === '!=') {
            flag |= NULL | UNDEFINED | VOID;
          }

          return isTypeFlagSet(type, flag);
        }
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `flag: ts.TypeFlags`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeFlagSet (from ../util)`
- **Internal Comments**:
```
// Allow comparison to `any`, `unknown` or a naked type parameter. (x3)
// Allow loose comparison to nullish values.
```

### `checkLogicalExpressionForUnnecessaryConditionals(node: TSESTree.LogicalExpression): void`

<details><summary>Code</summary>

```ts
function checkLogicalExpressionForUnnecessaryConditionals(
      node: TSESTree.LogicalExpression,
    ): void {
      if (node.operator === '??') {
        checkNodeForNullish(node.left);
        return;
      }
      // Only checks the left side, since the right side might not be "conditional" at all.
      // The right side will be checked if the LogicalExpression is used in a conditional context
      checkNode(node.left);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks that a logical expression contains a boolean, reports otherwise.
     */
```

- **Parameters**:
  - `node: TSESTree.LogicalExpression`
- **Return Type**: `void`
- **Calls**:
  - `checkNodeForNullish`
  - `checkNode`
- **Internal Comments**:
```
// Only checks the left side, since the right side might not be "conditional" at all. (x3)
// The right side will be checked if the LogicalExpression is used in a conditional context (x3)
```

### `checkIfWhileLoopIsNecessaryConditional(node: TSESTree.WhileStatement): void`

<details><summary>Code</summary>

```ts
function checkIfWhileLoopIsNecessaryConditional(
      node: TSESTree.WhileStatement,
    ): void {
      if (
        allowConstantLoopConditionsOption === 'only-allowed-literals' &&
        node.test.type === AST_NODE_TYPES.Literal &&
        constantLoopConditionsAllowedLiterals.has(node.test.value)
      ) {
        return;
      }

      checkIfLoopIsNecessaryConditional(node);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.WhileStatement`
- **Return Type**: `void`
- **Calls**:
  - `constantLoopConditionsAllowedLiterals.has`
  - `checkIfLoopIsNecessaryConditional`
### `checkIfLoopIsNecessaryConditional(node: | TSESTree.DoWhileStatement
        | TSESTree.ForStatement
        | TSESTree.WhileStatement): void`

<details><summary>Code</summary>

```ts
function checkIfLoopIsNecessaryConditional(
      node:
        | TSESTree.DoWhileStatement
        | TSESTree.ForStatement
        | TSESTree.WhileStatement,
    ): void {
      if (node.test == null) {
        // e.g. `for(;;)`
        return;
      }

      if (
        allowConstantLoopConditionsOption === 'always' &&
        tsutils.isTrueLiteralType(
          getConstrainedTypeAtLocation(services, node.test),
        )
      ) {
        return;
      }

      checkNode(node.test);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks that a testable expression of a loop is necessarily conditional, reports otherwise.
     */
```

- **Parameters**:
  - `node: | TSESTree.DoWhileStatement
        | TSESTree.ForStatement
        | TSESTree.WhileStatement`
- **Return Type**: `void`
- **Calls**:
  - `tsutils.isTrueLiteralType`
  - `getConstrainedTypeAtLocation (from ../util)`
  - `checkNode`
- **Internal Comments**:
```
// e.g. `for(;;)`
```

### `checkCallExpression(node: TSESTree.CallExpression): void`

<details><summary>Code</summary>

```ts
function checkCallExpression(node: TSESTree.CallExpression): void {
      if (checkTypePredicates) {
        const truthinessAssertedArgument = findTruthinessAssertedArgument(
          services,
          node,
        );
        if (truthinessAssertedArgument != null) {
          checkNode(truthinessAssertedArgument);
        }

        const typeGuardAssertedArgument = findTypeGuardAssertedArgument(
          services,
          node,
        );
        if (typeGuardAssertedArgument != null) {
          const typeOfArgument = getConstrainedTypeAtLocation(
            services,
            typeGuardAssertedArgument.argument,
          );
          if (typeOfArgument === typeGuardAssertedArgument.type) {
            context.report({
              node: typeGuardAssertedArgument.argument,
              messageId: 'typeGuardAlreadyIsType',
              data: {
                typeGuardOrAssertionFunction: typeGuardAssertedArgument.asserts
                  ? 'assertion function'
                  : 'type guard',
              },
            });
          }
        }
      }

      // If this is something like arr.filter(x => /*condition*/), check `condition`
      if (
        isArrayMethodCallWithPredicate(context, services, node) &&
        node.arguments.length
      ) {
        const callback = node.arguments[0];
        // Inline defined functions
        if (
          callback.type === AST_NODE_TYPES.ArrowFunctionExpression ||
          callback.type === AST_NODE_TYPES.FunctionExpression
        ) {
          // Two special cases, where we can directly check the node that's returned:
          // () => something
          if (callback.body.type !== AST_NODE_TYPES.BlockStatement) {
            return checkNode(callback.body);
          }
          // () => { return something; }
          const callbackBody = callback.body.body;
          if (
            callbackBody.length === 1 &&
            callbackBody[0].type === AST_NODE_TYPES.ReturnStatement &&
            callbackBody[0].argument
          ) {
            return checkNode(callbackBody[0].argument);
          }
          // Potential enhancement: could use code-path analysis to check
          //   any function with a single return statement
          // (Value to complexity ratio is dubious however)
        }
        // Otherwise just do type analysis on the function as a whole.
        const returnTypes = tsutils
          .getCallSignaturesOfType(
            getConstrainedTypeAtLocation(services, callback),
          )
          .map(sig => sig.getReturnType());

        if (returnTypes.length === 0) {
          // Not a callable function, e.g. `any`
          return;
        }

        let hasFalsyReturnTypes = false;
        let hasTruthyReturnTypes = false;

        for (const type of returnTypes) {
          const { constraintType } = getConstraintInfo(checker, type);
          // Predicate is always necessary if it involves `any` or `unknown`
          if (
            !constraintType ||
            isTypeAnyType(constraintType) ||
            isTypeUnknownType(constraintType)
          ) {
            return;
          }

          if (isPossiblyFalsy(constraintType)) {
            hasFalsyReturnTypes = true;
          }

          if (isPossiblyTruthy(constraintType)) {
            hasTruthyReturnTypes = true;
          }

          // bail early if both a possibly-truthy and a possibly-falsy have been detected
          if (hasFalsyReturnTypes && hasTruthyReturnTypes) {
            return;
          }
        }

        if (!hasFalsyReturnTypes) {
          return context.report({
            node: callback,
            messageId: 'alwaysTruthyFunc',
          });
        }

        if (!hasTruthyReturnTypes) {
          return context.report({
            node: callback,
            messageId: 'alwaysFalsyFunc',
          });
        }
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression`
- **Return Type**: `void`
- **Calls**:
  - `findTruthinessAssertedArgument (from ../util/assertionFunctionUtils)`
  - `checkNode`
  - `findTypeGuardAssertedArgument (from ../util/assertionFunctionUtils)`
  - `getConstrainedTypeAtLocation (from ../util)`
  - `context.report`
  - `isArrayMethodCallWithPredicate (from ../util)`
  - `tsutils
          .getCallSignaturesOfType(
            getConstrainedTypeAtLocation(services, callback),
          )
          .map`
  - `sig.getReturnType`
  - `getConstraintInfo (from ../util)`
  - `isTypeAnyType (from ../util)`
  - `isTypeUnknownType (from ../util)`
  - `isPossiblyFalsy (from ../util)`
  - `isPossiblyTruthy (from ../util)`
- **Internal Comments**:
```
// If this is something like arr.filter(x => /*condition*/), check `condition`
// Inline defined functions
// Two special cases, where we can directly check the node that's returned:
// () => something
// () => { return something; } (x2)
// Otherwise just do type analysis on the function as a whole. (x2)
// Not a callable function, e.g. `any`
// Predicate is always necessary if it involves `any` or `unknown`
// bail early if both a possibly-truthy and a possibly-falsy have been detected
```

### `optionChainContainsOptionArrayIndex(node: TSESTree.CallExpression | TSESTree.MemberExpression): boolean`

<details><summary>Code</summary>

```ts
function optionChainContainsOptionArrayIndex(
      node: TSESTree.CallExpression | TSESTree.MemberExpression,
    ): boolean {
      const lhsNode =
        node.type === AST_NODE_TYPES.CallExpression ? node.callee : node.object;
      if (node.optional && isArrayIndexExpression(lhsNode)) {
        return true;
      }
      if (
        lhsNode.type === AST_NODE_TYPES.MemberExpression ||
        lhsNode.type === AST_NODE_TYPES.CallExpression
      ) {
        return optionChainContainsOptionArrayIndex(lhsNode);
      }
      return false;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression | TSESTree.MemberExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `isArrayIndexExpression`
  - `optionChainContainsOptionArrayIndex`
### `isNullablePropertyType(objType: ts.Type, propertyType: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isNullablePropertyType(
      objType: ts.Type,
      propertyType: ts.Type,
    ): boolean {
      if (propertyType.isUnion()) {
        return propertyType.types.some(type =>
          isNullablePropertyType(objType, type),
        );
      }
      if (propertyType.isNumberLiteral() || propertyType.isStringLiteral()) {
        const propType = getTypeOfPropertyOfName(
          checker,
          objType,
          propertyType.value.toString(),
        );
        if (propType) {
          return isNullableType(propType);
        }
      }
      const typeName = getTypeName(checker, propertyType);
      return checker
        .getIndexInfosOfType(objType)
        .some(info => getTypeName(checker, info.keyType) === typeName);
    }
```
</details>

- **Parameters**:
  - `objType: ts.Type`
  - `propertyType: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `propertyType.isUnion`
  - `propertyType.types.some`
  - `isNullablePropertyType`
  - `propertyType.isNumberLiteral`
  - `propertyType.isStringLiteral`
  - `getTypeOfPropertyOfName (from ../util)`
  - `propertyType.value.toString`
  - `isNullableType (from ../util)`
  - `getTypeName (from ../util)`
  - `checker
        .getIndexInfosOfType(objType)
        .some`
### `isMemberExpressionNullableOriginFromObject(node: TSESTree.MemberExpression): boolean`

<details><summary>Code</summary>

```ts
function isMemberExpressionNullableOriginFromObject(
      node: TSESTree.MemberExpression,
    ): boolean {
      const prevType = getConstrainedTypeAtLocation(services, node.object);
      const property = node.property;
      if (prevType.isUnion() && isIdentifier(property)) {
        const isOwnNullable = prevType.types.some(type => {
          if (node.computed) {
            const propertyType = getConstrainedTypeAtLocation(
              services,
              node.property,
            );
            return isNullablePropertyType(type, propertyType);
          }
          const propType = getTypeOfPropertyOfName(
            checker,
            type,
            property.name,
          );

          if (propType) {
            return isNullableType(propType);
          }
          const indexInfo = checker.getIndexInfosOfType(type);

          return indexInfo.some(info => {
            const isStringTypeName =
              getTypeName(checker, info.keyType) === 'string';

            return (
              isStringTypeName &&
              (isNoUncheckedIndexedAccess || isNullableType(info.type))
            );
          });
        });
        return !isOwnNullable && isNullableType(prevType);
      }
      return false;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.MemberExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `prevType.isUnion`
  - `isIdentifier (from ../util)`
  - `prevType.types.some`
  - `isNullablePropertyType`
  - `getTypeOfPropertyOfName (from ../util)`
  - `isNullableType (from ../util)`
  - `checker.getIndexInfosOfType`
  - `indexInfo.some`
  - `getTypeName (from ../util)`
### `isCallExpressionNullableOriginFromCallee(node: TSESTree.CallExpression): boolean`

<details><summary>Code</summary>

```ts
function isCallExpressionNullableOriginFromCallee(
      node: TSESTree.CallExpression,
    ): boolean {
      const prevType = getConstrainedTypeAtLocation(services, node.callee);

      if (prevType.isUnion()) {
        const isOwnNullable = prevType.types.some(type => {
          const signatures = type.getCallSignatures();
          return signatures.some(sig => isNullableType(sig.getReturnType()));
        });
        return !isOwnNullable && isNullableType(prevType);
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `prevType.isUnion`
  - `prevType.types.some`
  - `type.getCallSignatures`
  - `signatures.some`
  - `isNullableType (from ../util)`
  - `sig.getReturnType`
### `isOptionableExpression(node: TSESTree.Expression): boolean`

<details><summary>Code</summary>

```ts
function isOptionableExpression(node: TSESTree.Expression): boolean {
      const type = getConstrainedTypeAtLocation(services, node);
      const isOwnNullable =
        node.type === AST_NODE_TYPES.MemberExpression
          ? !isMemberExpressionNullableOriginFromObject(node)
          : node.type === AST_NODE_TYPES.CallExpression
            ? !isCallExpressionNullableOriginFromCallee(node)
            : true;

      return (
        isConditionalAlwaysNecessary(type) ||
        (isOwnNullable && isNullableType(type))
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `boolean`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `isMemberExpressionNullableOriginFromObject`
  - `isCallExpressionNullableOriginFromCallee`
  - `isConditionalAlwaysNecessary`
  - `isNullableType (from ../util)`
### `checkOptionalChain(node: TSESTree.CallExpression | TSESTree.MemberExpression, beforeOperator: TSESTree.Node, fix: '' | '.'): void`

<details><summary>Code</summary>

```ts
function checkOptionalChain(
      node: TSESTree.CallExpression | TSESTree.MemberExpression,
      beforeOperator: TSESTree.Node,
      fix: '' | '.',
    ): void {
      // We only care if this step in the chain is optional. If just descend
      // from an optional chain, then that's fine.
      if (!node.optional) {
        return;
      }

      // Since typescript array index signature types don't represent the
      //  possibility of out-of-bounds access, if we're indexing into an array
      //  just skip the check, to avoid false positives
      if (
        !isNoUncheckedIndexedAccess &&
        optionChainContainsOptionArrayIndex(node)
      ) {
        return;
      }

      const nodeToCheck =
        node.type === AST_NODE_TYPES.CallExpression ? node.callee : node.object;

      if (isOptionableExpression(nodeToCheck)) {
        return;
      }

      const questionDotOperator = nullThrows(
        context.sourceCode.getTokenAfter(
          beforeOperator,
          token =>
            token.type === AST_TOKEN_TYPES.Punctuator && token.value === '?.',
        ),
        NullThrowsReasons.MissingToken('operator', node.type),
      );

      context.report({
        loc: questionDotOperator.loc,
        node,
        messageId: 'neverOptionalChain',
        suggest: [
          {
            messageId: 'suggestRemoveOptionalChain',
            fix(fixer) {
              return fixer.replaceText(questionDotOperator, fix);
            },
          },
        ],
      });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression | TSESTree.MemberExpression`
  - `beforeOperator: TSESTree.Node`
  - `fix: '' | '.'`
- **Return Type**: `void`
- **Calls**:
  - `optionChainContainsOptionArrayIndex`
  - `isOptionableExpression`
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenAfter`
  - `NullThrowsReasons.MissingToken`
  - `context.report`
  - `fixer.replaceText`
- **Internal Comments**:
```
// We only care if this step in the chain is optional. If just descend
// from an optional chain, then that's fine.
// Since typescript array index signature types don't represent the
//  possibility of out-of-bounds access, if we're indexing into an array
//  just skip the check, to avoid false positives
```

### `checkOptionalMemberExpression(node: TSESTree.MemberExpression): void`

<details><summary>Code</summary>

```ts
function checkOptionalMemberExpression(
      node: TSESTree.MemberExpression,
    ): void {
      checkOptionalChain(node, node.object, node.computed ? '' : '.');
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.MemberExpression`
- **Return Type**: `void`
- **Calls**:
  - `checkOptionalChain`
### `checkOptionalCallExpression(node: TSESTree.CallExpression): void`

<details><summary>Code</summary>

```ts
function checkOptionalCallExpression(node: TSESTree.CallExpression): void {
      checkOptionalChain(node, node.callee, '');
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression`
- **Return Type**: `void`
- **Calls**:
  - `checkOptionalChain`
### `checkAssignmentExpression(node: TSESTree.AssignmentExpression): void`

<details><summary>Code</summary>

```ts
function checkAssignmentExpression(
      node: TSESTree.AssignmentExpression,
    ): void {
      // Similar to checkLogicalExpressionForUnnecessaryConditionals, since
      // a ||= b is equivalent to a || (a = b)
      if (['&&=', '||='].includes(node.operator)) {
        checkNode(node.left);
      } else if (node.operator === '??=') {
        checkNodeForNullish(node.left);
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.AssignmentExpression`
- **Return Type**: `void`
- **Calls**:
  - `['&&=', '||='].includes`
  - `checkNode`
  - `checkNodeForNullish`
- **Internal Comments**:
```
// Similar to checkLogicalExpressionForUnnecessaryConditionals, since
// a ||= b is equivalent to a || (a = b)
```

### `ConditionalExpression(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => checkNode(node.test)
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkNode`
### `IfStatement(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => checkNode(node.test)
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkNode`
### `ConditionalExpression(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => checkNode(node.test)
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkNode`
### `IfStatement(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => checkNode(node.test)
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkNode`
### `ConditionalExpression(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => checkNode(node.test)
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkNode`
### `IfStatement(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => checkNode(node.test)
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkNode`
### `ConditionalExpression(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => checkNode(node.test)
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkNode`
### `IfStatement(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => checkNode(node.test)
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkNode`
### `normalizeAllowConstantLoopConditions(allowConstantLoopConditions: | AllowConstantLoopConditions
    | LegacyAllowConstantLoopConditions): AllowConstantLoopConditions`

<details><summary>Code</summary>

```ts
function normalizeAllowConstantLoopConditions(
  allowConstantLoopConditions:
    | AllowConstantLoopConditions
    | LegacyAllowConstantLoopConditions,
): AllowConstantLoopConditions {
  if (allowConstantLoopConditions === true) {
    return 'always';
  }

  if (allowConstantLoopConditions === false) {
    return 'never';
  }

  return allowConstantLoopConditions;
}
```
</details>

- **Parameters**:
  - `allowConstantLoopConditions: | AllowConstantLoopConditions
    | LegacyAllowConstantLoopConditions`
- **Return Type**: `AllowConstantLoopConditions`

---

## Type Aliases

### `BoolOperator`

```ts
type BoolOperator = typeof BOOL_OPERATORS extends Set<infer T> ? T : never;
```

### `LegacyAllowConstantLoopConditions`

```ts
type LegacyAllowConstantLoopConditions = boolean;
```

### `AllowConstantLoopConditions`

```ts
type AllowConstantLoopConditions = 'always' | 'never' | 'only-allowed-literals';
```

### `Options`

```ts
type Options = [
  {
    allowConstantLoopConditions?:
      | AllowConstantLoopConditions
      | LegacyAllowConstantLoopConditions;
    allowRuleToRunWithoutStrictNullChecksIKnowWhatIAmDoing?: boolean;
    checkTypePredicates?: boolean;
  },
];
```

### `MessageId`

```ts
type MessageId = | 'alwaysFalsy'
  | 'alwaysFalsyFunc'
  | 'alwaysNullish'
  | 'alwaysTruthy'
  | 'alwaysTruthyFunc'
  | 'comparisonBetweenLiteralTypes'
  | 'never'
  | 'neverNullish'
  | 'neverOptionalChain'
  | 'noOverlapBooleanExpression'
  | 'noStrictNullCheck'
  | 'suggestRemoveOptionalChain'
  | 'typeGuardAlreadyIsType';
```


---