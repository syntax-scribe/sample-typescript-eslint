[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-nullish-coalescing.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 16
- **Classes**: 0
- **Imports**: 21
- **Interfaces**: 0
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-nullish-coalescing.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `getTextWithParentheses` | `../util` |
| `getTypeFlags` | `../util` |
| `isLogicalOrOperator` | `../util` |
| `isNodeEqual` | `../util` |
| `isNodeOfTypes` | `../util` |
| `isNullLiteral` | `../util` |
| `isNullableType` | `../util` |
| `isUndefinedIdentifier` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |
| `skipChainExpression` | `../util` |
| `isParenthesized` | `../util` |
| `getOperatorPrecedenceForNode` | `../util` |
| `OperatorPrecedence` | `../util` |
| `getWrappedCode` | `../util/getWrappedCode` |


---

## Functions

### `isNullLiteralOrUndefinedIdentifier(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
(node: TSESTree.Node): boolean =>
  isNullLiteral(node) || isUndefinedIdentifier(node)
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `isNodeNullishComparison(node: TSESTree.BinaryExpression): boolean`

<details><summary>Code</summary>

```ts
(node: TSESTree.BinaryExpression): boolean =>
  isNullLiteralOrUndefinedIdentifier(node.left) &&
  isNullLiteralOrUndefinedIdentifier(node.right)
```
</details>

- **Parameters**:
  - `node: TSESTree.BinaryExpression`
- **Return Type**: `boolean`
### `isTypeEligibleForPreferNullish(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isTypeEligibleForPreferNullish(type: ts.Type): boolean {
      if (!isNullableType(type)) {
        return false;
      }

      const ignorableFlags = [
        /* eslint-disable @typescript-eslint/no-non-null-assertion */
        (ignorePrimitives === true || ignorePrimitives!.bigint) &&
          ts.TypeFlags.BigIntLike,
        (ignorePrimitives === true || ignorePrimitives!.boolean) &&
          ts.TypeFlags.BooleanLike,
        (ignorePrimitives === true || ignorePrimitives!.number) &&
          ts.TypeFlags.NumberLike,
        (ignorePrimitives === true || ignorePrimitives!.string) &&
          ts.TypeFlags.StringLike,
        /* eslint-enable @typescript-eslint/no-non-null-assertion */
      ]
        .filter((flag): flag is number => typeof flag === 'number')
        .reduce((previous, flag) => previous | flag, 0);

      if (ignorableFlags === 0) {
        // any types are eligible for conversion.
        return true;
      }

      // if the type is `any` or `unknown` we can't make any assumptions
      // about the value, so it could be any primitive, even though the flags
      // won't be set.
      //
      // technically, this is true of `void` as well, however, it's a TS error
      // to test `void` for truthiness, so we don't need to bother checking for
      // it in valid code.
      if (
        tsutils.isTypeFlagSet(type, ts.TypeFlags.Any | ts.TypeFlags.Unknown)
      ) {
        return false;
      }

      if (
        tsutils
          .typeConstituents(type)
          .some(t =>
            tsutils
              .intersectionConstituents(t)
              .some(t => tsutils.isTypeFlagSet(t, ignorableFlags)),
          )
      ) {
        return false;
      }

      return true;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks whether a type tested for truthiness is eligible for conversion to
     * a nullishness check, taking into account the rule's configuration.
     */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isNullableType (from ../util)`
  - `[
        /* eslint-disable @typescript-eslint/no-non-null-assertion */
        (ignorePrimitives === true || ignorePrimitives!.bigint) &&
          ts.TypeFlags.BigIntLike,
        (ignorePrimitives === true || ignorePrimitives!.boolean) &&
          ts.TypeFlags.BooleanLike,
        (ignorePrimitives === true || ignorePrimitives!.number) &&
          ts.TypeFlags.NumberLike,
        (ignorePrimitives === true || ignorePrimitives!.string) &&
          ts.TypeFlags.StringLike,
        /* eslint-enable @typescript-eslint/no-non-null-assertion */
      ]
        .filter((flag): flag is number => typeof flag === 'number')
        .reduce`
  - `tsutils.isTypeFlagSet`
  - `tsutils
          .typeConstituents(type)
          .some`
  - `tsutils
              .intersectionConstituents(t)
              .some`
- **Internal Comments**:
```
/* eslint-disable @typescript-eslint/no-non-null-assertion */ (x2)
// any types are eligible for conversion.
// if the type is `any` or `unknown` we can't make any assumptions
// about the value, so it could be any primitive, even though the flags
// won't be set.
//
// technically, this is true of `void` as well, however, it's a TS error
// to test `void` for truthiness, so we don't need to bother checking for
// it in valid code.
```

### `isTruthinessCheckEligibleForPreferNullish({
      node,
      testNode,
    }: {
      node:
        | TSESTree.AssignmentExpression
        | TSESTree.ConditionalExpression
        | TSESTree.IfStatement
        | TSESTree.LogicalExpression;
      testNode: TSESTree.Node;
    }): boolean`

<details><summary>Code</summary>

```ts
function isTruthinessCheckEligibleForPreferNullish({
      node,
      testNode,
    }: {
      node:
        | TSESTree.AssignmentExpression
        | TSESTree.ConditionalExpression
        | TSESTree.IfStatement
        | TSESTree.LogicalExpression;
      testNode: TSESTree.Node;
    }): boolean {
      const testType = parserServices.getTypeAtLocation(testNode);
      if (!isTypeEligibleForPreferNullish(testType)) {
        return false;
      }

      if (ignoreConditionalTests === true && isConditionalTest(node)) {
        return false;
      }

      if (
        ignoreBooleanCoercion === true &&
        isBooleanConstructorContext(node, context)
      ) {
        return false;
      }

      return true;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Determines whether a control flow construct that uses the truthiness of
     * a test expression is eligible for conversion to the nullish coalescing
     * operator, taking into account (both dependent on the rule's configuration):
     * 1. Whether the construct is in a permitted syntactic context
     * 2. Whether the type of the test expression is deemed eligible for
     *    conversion
     *
     * @param node The overall node to be converted (e.g. `a || b` or `a ? a : b`)
     * @param testNode The node being tested (i.e. `a`)
     */
```

- **Parameters**:
  - `{
      node,
      testNode,
    }: {
      node:
        | TSESTree.AssignmentExpression
        | TSESTree.ConditionalExpression
        | TSESTree.IfStatement
        | TSESTree.LogicalExpression;
      testNode: TSESTree.Node;
    }`
- **Return Type**: `boolean`
- **Calls**:
  - `parserServices.getTypeAtLocation`
  - `isTypeEligibleForPreferNullish`
  - `isConditionalTest`
  - `isBooleanConstructorContext`
### `checkAndFixWithPreferNullishOverOr(node: TSESTree.AssignmentExpression | TSESTree.LogicalExpression, description: string, equals: string): void`

<details><summary>Code</summary>

```ts
function checkAndFixWithPreferNullishOverOr(
      node: TSESTree.AssignmentExpression | TSESTree.LogicalExpression,
      description: string,
      equals: string,
    ): void {
      if (
        !isTruthinessCheckEligibleForPreferNullish({
          node,
          testNode: node.left,
        })
      ) {
        return;
      }

      if (
        ignoreMixedLogicalExpressions === true &&
        isMixedLogicalExpression(node)
      ) {
        return;
      }

      const barBarOperator = nullThrows(
        context.sourceCode.getTokenAfter(
          node.left,
          token =>
            token.type === AST_TOKEN_TYPES.Punctuator &&
            token.value === node.operator,
        ),
        NullThrowsReasons.MissingToken('operator', node.type),
      );

      function* fix(
        fixer: TSESLint.RuleFixer,
      ): IterableIterator<TSESLint.RuleFix> {
        if (isLogicalOrOperator(node.parent)) {
          // '&&' and '??' operations cannot be mixed without parentheses (e.g. a && b ?? c)
          if (
            node.left.type === AST_NODE_TYPES.LogicalExpression &&
            !isLogicalOrOperator(node.left.left)
          ) {
            yield fixer.insertTextBefore(node.left.right, '(');
          } else {
            yield fixer.insertTextBefore(node.left, '(');
          }
          yield fixer.insertTextAfter(node.right, ')');
        }
        yield fixer.replaceText(
          barBarOperator,
          node.operator.replace('||', '??'),
        );
      }

      context.report({
        node: barBarOperator,
        messageId: 'preferNullishOverOr',
        data: { description, equals },
        suggest: [
          {
            messageId: 'suggestNullish',
            data: { equals },
            fix,
          },
        ],
      });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.AssignmentExpression | TSESTree.LogicalExpression`
  - `description: string`
  - `equals: string`
- **Return Type**: `void`
- **Calls**:
  - `isTruthinessCheckEligibleForPreferNullish`
  - `isMixedLogicalExpression`
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenAfter`
  - `NullThrowsReasons.MissingToken`
  - `isLogicalOrOperator (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
  - `fixer.replaceText`
  - `node.operator.replace`
  - `context.report`
- **Internal Comments**:
```
// '&&' and '??' operations cannot be mixed without parentheses (e.g. a && b ?? c)
```

### `fix(fixer: TSESLint.RuleFixer): IterableIterator<TSESLint.RuleFix>`

<details><summary>Code</summary>

```ts
function* fix(
        fixer: TSESLint.RuleFixer,
      ): IterableIterator<TSESLint.RuleFix> {
        if (isLogicalOrOperator(node.parent)) {
          // '&&' and '??' operations cannot be mixed without parentheses (e.g. a && b ?? c)
          if (
            node.left.type === AST_NODE_TYPES.LogicalExpression &&
            !isLogicalOrOperator(node.left.left)
          ) {
            yield fixer.insertTextBefore(node.left.right, '(');
          } else {
            yield fixer.insertTextBefore(node.left, '(');
          }
          yield fixer.insertTextAfter(node.right, ')');
        }
        yield fixer.replaceText(
          barBarOperator,
          node.operator.replace('||', '??'),
        );
      }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `IterableIterator<TSESLint.RuleFix>`
- **Calls**:
  - `isLogicalOrOperator (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
  - `fixer.replaceText`
  - `node.operator.replace`
- **Internal Comments**:
```
// '&&' and '??' operations cannot be mixed without parentheses (e.g. a && b ?? c)
```

### `getNullishCoalescingParams(node: TSESTree.ConditionalExpression | TSESTree.IfStatement, nonNullishNode: TSESTree.Expression, nodesInsideTestExpression: TSESTree.Node[], operator: NullishCheckOperator): | { isFixable: false }
      | { isFixable: true; nullishCoalescingLeftNode: TSESTree.Node }`

<details><summary>Code</summary>

```ts
function getNullishCoalescingParams(
      node: TSESTree.ConditionalExpression | TSESTree.IfStatement,
      nonNullishNode: TSESTree.Expression,
      nodesInsideTestExpression: TSESTree.Node[],
      operator: NullishCheckOperator,
    ):
      | { isFixable: false }
      | { isFixable: true; nullishCoalescingLeftNode: TSESTree.Node } {
      let nullishCoalescingLeftNode: TSESTree.Node | undefined;
      let hasTruthinessCheck = false;
      let hasNullCheckWithoutTruthinessCheck = false;
      let hasUndefinedCheckWithoutTruthinessCheck = false;

      if (!nodesInsideTestExpression.length) {
        hasTruthinessCheck = true;
        nullishCoalescingLeftNode =
          node.test.type === AST_NODE_TYPES.UnaryExpression
            ? node.test.argument
            : node.test;

        if (
          !areNodesSimilarMemberAccess(
            nullishCoalescingLeftNode,
            nonNullishNode,
          )
        ) {
          return { isFixable: false };
        }
      } else {
        // we check that the test only contains null, undefined and the identifier
        for (const testNode of nodesInsideTestExpression) {
          if (isNullLiteral(testNode)) {
            hasNullCheckWithoutTruthinessCheck = true;
          } else if (isUndefinedIdentifier(testNode)) {
            hasUndefinedCheckWithoutTruthinessCheck = true;
          } else if (areNodesSimilarMemberAccess(testNode, nonNullishNode)) {
            // Only consider the first expression in a multi-part nullish check,
            // as subsequent expressions might not require all the optional chaining operators.
            // For example: a?.b?.c !== undefined && a.b.c !== null ? a.b.c : 'foo';
            // This works because `node.test` is always evaluated first in the loop
            // and has the same or more necessary optional chaining operators
            // than `node.alternate` or `node.consequent`.
            nullishCoalescingLeftNode ??= testNode;
          } else {
            return { isFixable: false };
          }
        }
      }

      if (!nullishCoalescingLeftNode) {
        return { isFixable: false };
      }

      const isFixable = ((): boolean => {
        if (hasTruthinessCheck) {
          return isTruthinessCheckEligibleForPreferNullish({
            node,
            testNode: nullishCoalescingLeftNode,
          });
        }

        // it is fixable if we check for both null and undefined, or not if neither
        if (
          hasUndefinedCheckWithoutTruthinessCheck ===
          hasNullCheckWithoutTruthinessCheck
        ) {
          return hasUndefinedCheckWithoutTruthinessCheck;
        }

        // it is fixable if we loosely check for either null or undefined
        if (['==', '!='].includes(operator)) {
          return true;
        }

        const type = parserServices.getTypeAtLocation(
          nullishCoalescingLeftNode,
        );
        const flags = getTypeFlags(type);

        if (flags & (ts.TypeFlags.Any | ts.TypeFlags.Unknown)) {
          return false;
        }

        const hasNullType = (flags & ts.TypeFlags.Null) !== 0;

        // it is fixable if we check for undefined and the type is not nullable
        if (hasUndefinedCheckWithoutTruthinessCheck && !hasNullType) {
          return true;
        }

        const hasUndefinedType = (flags & ts.TypeFlags.Undefined) !== 0;

        // it is fixable if we check for null and the type can't be undefined
        return hasNullCheckWithoutTruthinessCheck && !hasUndefinedType;
      })();

      return isFixable
        ? { isFixable: true, nullishCoalescingLeftNode }
        : { isFixable: false };
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.ConditionalExpression | TSESTree.IfStatement`
  - `nonNullishNode: TSESTree.Expression`
  - `nodesInsideTestExpression: TSESTree.Node[]`
  - `operator: NullishCheckOperator`
- **Return Type**: `| { isFixable: false }
      | { isFixable: true; nullishCoalescingLeftNode: TSESTree.Node }`
- **Calls**:
  - `areNodesSimilarMemberAccess`
  - `isNullLiteral (from ../util)`
  - `isUndefinedIdentifier (from ../util)`
  - `complex_call_14038`
  - `isTruthinessCheckEligibleForPreferNullish`
  - `['==', '!='].includes`
  - `parserServices.getTypeAtLocation`
  - `getTypeFlags (from ../util)`
- **Internal Comments**:
```
// we check that the test only contains null, undefined and the identifier
// Only consider the first expression in a multi-part nullish check, (x3)
// as subsequent expressions might not require all the optional chaining operators. (x3)
// For example: a?.b?.c !== undefined && a.b.c !== null ? a.b.c : 'foo'; (x3)
// This works because `node.test` is always evaluated first in the loop (x3)
// and has the same or more necessary optional chaining operators (x3)
// than `node.alternate` or `node.consequent`. (x3)
// it is fixable if we check for both null and undefined, or not if neither
// it is fixable if we loosely check for either null or undefined
// it is fixable if we check for undefined and the type is not nullable
// it is fixable if we check for null and the type can't be undefined
```

### `isConditionalTest(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isConditionalTest(node: TSESTree.Node): boolean {
  const parent = node.parent;
  if (parent == null) {
    return false;
  }

  if (parent.type === AST_NODE_TYPES.LogicalExpression) {
    return isConditionalTest(parent);
  }

  if (
    parent.type === AST_NODE_TYPES.ConditionalExpression &&
    (parent.consequent === node || parent.alternate === node)
  ) {
    return isConditionalTest(parent);
  }

  if (
    parent.type === AST_NODE_TYPES.SequenceExpression &&
    parent.expressions.at(-1) === node
  ) {
    return isConditionalTest(parent);
  }

  if (
    parent.type === AST_NODE_TYPES.UnaryExpression &&
    parent.operator === '!'
  ) {
    return isConditionalTest(parent);
  }

  if (
    (parent.type === AST_NODE_TYPES.ConditionalExpression ||
      parent.type === AST_NODE_TYPES.DoWhileStatement ||
      parent.type === AST_NODE_TYPES.IfStatement ||
      parent.type === AST_NODE_TYPES.ForStatement ||
      parent.type === AST_NODE_TYPES.WhileStatement) &&
    parent.test === node
  ) {
    return true;
  }

  return false;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isConditionalTest`
  - `parent.expressions.at`
### `isBooleanConstructorContext(node: TSESTree.Node, context: Readonly<TSESLint.RuleContext<MessageIds, Options>>): boolean`

<details><summary>Code</summary>

```ts
function isBooleanConstructorContext(
  node: TSESTree.Node,
  context: Readonly<TSESLint.RuleContext<MessageIds, Options>>,
): boolean {
  const parent = node.parent;
  if (parent == null) {
    return false;
  }

  if (parent.type === AST_NODE_TYPES.LogicalExpression) {
    return isBooleanConstructorContext(parent, context);
  }

  if (
    parent.type === AST_NODE_TYPES.ConditionalExpression &&
    (parent.consequent === node || parent.alternate === node)
  ) {
    return isBooleanConstructorContext(parent, context);
  }

  if (
    parent.type === AST_NODE_TYPES.SequenceExpression &&
    parent.expressions.at(-1) === node
  ) {
    return isBooleanConstructorContext(parent, context);
  }

  return isBuiltInBooleanCall(parent, context);
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `context: Readonly<TSESLint.RuleContext<MessageIds, Options>>`
- **Return Type**: `boolean`
- **Calls**:
  - `isBooleanConstructorContext`
  - `parent.expressions.at`
  - `isBuiltInBooleanCall`
### `isBuiltInBooleanCall(node: TSESTree.Node, context: Readonly<TSESLint.RuleContext<MessageIds, Options>>): boolean`

<details><summary>Code</summary>

```ts
function isBuiltInBooleanCall(
  node: TSESTree.Node,
  context: Readonly<TSESLint.RuleContext<MessageIds, Options>>,
): boolean {
  if (
    node.type === AST_NODE_TYPES.CallExpression &&
    node.callee.type === AST_NODE_TYPES.Identifier &&
    // eslint-disable-next-line @typescript-eslint/internal/prefer-ast-types-enum
    node.callee.name === 'Boolean' &&
    node.arguments[0]
  ) {
    const scope = context.sourceCode.getScope(node);
    const variable = scope.set.get(AST_TOKEN_TYPES.Boolean);
    return variable == null || variable.defs.length === 0;
  }
  return false;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `context: Readonly<TSESLint.RuleContext<MessageIds, Options>>`
- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode.getScope`
  - `scope.set.get`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/internal/prefer-ast-types-enum (x4)
```

### `isMixedLogicalExpression(node: TSESTree.AssignmentExpression | TSESTree.LogicalExpression): boolean`

<details><summary>Code</summary>

```ts
function isMixedLogicalExpression(
  node: TSESTree.AssignmentExpression | TSESTree.LogicalExpression,
): boolean {
  const seen = new Set<TSESTree.Node | undefined>();
  const queue = [node.parent, node.left, node.right];
  for (const current of queue) {
    if (seen.has(current)) {
      continue;
    }
    seen.add(current);

    if (current.type === AST_NODE_TYPES.LogicalExpression) {
      if (current.operator === '&&') {
        return true;
      }

      if (['||', '||='].includes(current.operator)) {
        // check the pieces of the node to catch cases like `a || b || c && d`
        queue.push(current.parent, current.left, current.right);
      }
    }
  }

  return false;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.AssignmentExpression | TSESTree.LogicalExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `seen.has`
  - `seen.add`
  - `['||', '||='].includes`
  - `queue.push`
- **Internal Comments**:
```
// check the pieces of the node to catch cases like `a || b || c && d` (x4)
```

### `areNodesSimilarMemberAccess(a: TSESTree.Node, b: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function areNodesSimilarMemberAccess(
  a: TSESTree.Node,
  b: TSESTree.Node,
): boolean {
  if (
    a.type === AST_NODE_TYPES.MemberExpression &&
    b.type === AST_NODE_TYPES.MemberExpression
  ) {
    if (!areNodesSimilarMemberAccess(a.object, b.object)) {
      return false;
    }

    if (a.computed === b.computed) {
      return isNodeEqual(a.property, b.property);
    }
    if (
      a.property.type === AST_NODE_TYPES.Literal &&
      b.property.type === AST_NODE_TYPES.Identifier
    ) {
      return a.property.value === b.property.name;
    }
    if (
      a.property.type === AST_NODE_TYPES.Identifier &&
      b.property.type === AST_NODE_TYPES.Literal
    ) {
      return a.property.name === b.property.value;
    }
    return false;
  }
  if (
    a.type === AST_NODE_TYPES.ChainExpression ||
    b.type === AST_NODE_TYPES.ChainExpression
  ) {
    return areNodesSimilarMemberAccess(
      skipChainExpression(a),
      skipChainExpression(b),
    );
  }
  return isNodeEqual(a, b);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if two TSESTree nodes have the same member access sequence,
 * regardless of optional chaining differences.
 *
 * Note: This does not imply that the nodes are runtime-equivalent.
 *
 * Example: `a.b.c`, `a?.b.c`, `a.b?.c`, `(a?.b).c`, `(a.b)?.c` are considered similar.
 *
 * @param a First TSESTree node.
 * @param b Second TSESTree node.
 * @returns `true` if the nodes access members in the same order; otherwise, `false`.
 */
```

- **Parameters**:
  - `a: TSESTree.Node`
  - `b: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `areNodesSimilarMemberAccess`
  - `isNodeEqual (from ../util)`
  - `skipChainExpression (from ../util)`
### `getBranchNodes(node: TSESTree.ConditionalExpression, operator: NullishCheckOperator): {
  nonNullishBranch: TSESTree.Expression;
  nullishBranch: TSESTree.Expression;
}`

<details><summary>Code</summary>

```ts
function getBranchNodes(
  node: TSESTree.ConditionalExpression,
  operator: NullishCheckOperator,
): {
  nonNullishBranch: TSESTree.Expression;
  nullishBranch: TSESTree.Expression;
} {
  if (['', '!=', '!=='].includes(operator)) {
    return { nonNullishBranch: node.consequent, nullishBranch: node.alternate };
  }
  return { nonNullishBranch: node.alternate, nullishBranch: node.consequent };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns the branch nodes of a conditional expression:
 * - the "nonNullish branch" is the branch when test node is not nullish
 * - the "nullish branch" is the branch when test node is nullish
 */
```

- **Parameters**:
  - `node: TSESTree.ConditionalExpression`
  - `operator: NullishCheckOperator`
- **Return Type**: `{
  nonNullishBranch: TSESTree.Expression;
  nullishBranch: TSESTree.Expression;
}`
- **Calls**:
  - `['', '!=', '!=='].includes`
### `getOperatorAndNodesInsideTestExpression(node: TSESTree.ConditionalExpression | TSESTree.IfStatement): {
  nodesInsideTestExpression: TSESTree.Node[];
  operator: NullishCheckOperator | null;
}`

<details><summary>Code</summary>

```ts
function getOperatorAndNodesInsideTestExpression(
  node: TSESTree.ConditionalExpression | TSESTree.IfStatement,
): {
  nodesInsideTestExpression: TSESTree.Node[];
  operator: NullishCheckOperator | null;
} {
  let operator: NullishCheckOperator | null = null;
  let nodesInsideTestExpression: TSESTree.Node[] = [];

  if (
    isMemberAccessLike(node.test) ||
    node.test.type === AST_NODE_TYPES.UnaryExpression
  ) {
    operator = getNonBinaryNodeOperator(node.test);
  } else if (node.test.type === AST_NODE_TYPES.BinaryExpression) {
    nodesInsideTestExpression = [node.test.left, node.test.right];
    if (
      node.test.operator === '==' ||
      node.test.operator === '!=' ||
      node.test.operator === '===' ||
      node.test.operator === '!=='
    ) {
      operator = node.test.operator;
    }
  } else if (
    node.test.type === AST_NODE_TYPES.LogicalExpression &&
    node.test.left.type === AST_NODE_TYPES.BinaryExpression &&
    node.test.right.type === AST_NODE_TYPES.BinaryExpression
  ) {
    if (
      isNodeNullishComparison(node.test.left) ||
      isNodeNullishComparison(node.test.right)
    ) {
      return { nodesInsideTestExpression, operator };
    }
    nodesInsideTestExpression = [
      node.test.left.left,
      node.test.left.right,
      node.test.right.left,
      node.test.right.right,
    ];
    if (['||', '||='].includes(node.test.operator)) {
      if (
        node.test.left.operator === '===' &&
        node.test.right.operator === '==='
      ) {
        operator = '===';
      } else if (
        ((node.test.left.operator === '===' ||
          node.test.right.operator === '===') &&
          (node.test.left.operator === '==' ||
            node.test.right.operator === '==')) ||
        (node.test.left.operator === '==' && node.test.right.operator === '==')
      ) {
        operator = '==';
      }
    } else if (node.test.operator === '&&') {
      if (
        node.test.left.operator === '!==' &&
        node.test.right.operator === '!=='
      ) {
        operator = '!==';
      } else if (
        ((node.test.left.operator === '!==' ||
          node.test.right.operator === '!==') &&
          (node.test.left.operator === '!=' ||
            node.test.right.operator === '!=')) ||
        (node.test.left.operator === '!=' && node.test.right.operator === '!=')
      ) {
        operator = '!=';
      }
    }
  }

  return { nodesInsideTestExpression, operator };
}
```
</details>

- **Parameters**:
  - `node: TSESTree.ConditionalExpression | TSESTree.IfStatement`
- **Return Type**: `{
  nodesInsideTestExpression: TSESTree.Node[];
  operator: NullishCheckOperator | null;
}`
- **Calls**:
  - `isMemberAccessLike`
  - `getNonBinaryNodeOperator`
  - `isNodeNullishComparison`
  - `['||', '||='].includes`
### `getNonBinaryNodeOperator(node: | TSESTree.ChainExpression
    | TSESTree.Identifier
    | TSESTree.MemberExpression
    | TSESTree.UnaryExpression): NullishCheckOperator | null`

<details><summary>Code</summary>

```ts
function getNonBinaryNodeOperator(
  node:
    | TSESTree.ChainExpression
    | TSESTree.Identifier
    | TSESTree.MemberExpression
    | TSESTree.UnaryExpression,
): NullishCheckOperator | null {
  if (node.type !== AST_NODE_TYPES.UnaryExpression) {
    return '';
  }
  if (isMemberAccessLike(node.argument) && node.operator === '!') {
    return '!';
  }
  return null;
}
```
</details>

- **Parameters**:
  - `node: | TSESTree.ChainExpression
    | TSESTree.Identifier
    | TSESTree.MemberExpression
    | TSESTree.UnaryExpression`
- **Return Type**: `NullishCheckOperator | null`
- **Calls**:
  - `isMemberAccessLike`
### `formatComments(comments: TSESTree.Comment[], separator: string): string`

<details><summary>Code</summary>

```ts
function formatComments(
  comments: TSESTree.Comment[],
  separator: string,
): string {
  return comments
    .map(({ type, value }) =>
      type === AST_TOKEN_TYPES.Line
        ? `//${value}${separator}`
        : `/*${value}*/${separator}`,
    )
    .join('');
}
```
</details>

- **Parameters**:
  - `comments: TSESTree.Comment[]`
  - `separator: string`
- **Return Type**: `string`
- **Calls**:
  - `comments
    .map(({ type, value }) =>
      type === AST_TOKEN_TYPES.Line
        ? `//${value}${separator}`
        : `/*${value}*/${separator}`,
    )
    .join`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `NullishCheckOperator`

```ts
type NullishCheckOperator = '!' | '!=' | '!==' | '' | '==' | '===';
```

### `Options`

```ts
type Options = [
  {
    allowRuleToRunWithoutStrictNullChecksIKnowWhatIAmDoing?: boolean;
    ignoreBooleanCoercion?: boolean;
    ignoreConditionalTests?: boolean;
    ignoreIfStatements?: boolean;
    ignoreMixedLogicalExpressions?: boolean;
    ignorePrimitives?:
      | true
      | {
          bigint?: boolean;
          boolean?: boolean;
          number?: boolean;
          string?: boolean;
        };
    ignoreTernaryTests?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = | 'noStrictNullCheck'
  | 'preferNullishOverAssignment'
  | 'preferNullishOverOr'
  | 'preferNullishOverTernary'
  | 'suggestNullish';
```


---