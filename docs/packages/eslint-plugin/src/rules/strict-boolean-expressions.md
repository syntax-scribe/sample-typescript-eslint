[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `strict-boolean-expressions.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 299 |
| 🧱 Classes | 0 |
| 📦 Imports | 14 |
| 📊 Variables & Constants | 4 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 5 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/strict-boolean-expressions.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserServicesWithTypeInformation` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `ReportSuggestionArray` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ASTUtils` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `getWrappingFixer` | `../util` |
| `isArrayMethodCallWithPredicate` | `../util` |
| `isParenlessArrowFunction` | `../util` |
| `isTypeArrayTypeOrUnionOfArrayTypes` | `../util` |
| `nullThrows` | `../util` |
| `findTruthinessAssertedArgument` | `../util/assertionFunctionUtils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `traversedNodes` | `Set<TSESTree.Node>` | const | `new Set<TSESTree.Node>()` | ✗ |
| `flattenTypes` | `unknown[]` | const | `[
        ...new Set(
          returnTypes.flatMap(type => tsutils.unionConstituents(type)),
        ),
      ]` | ✗ |
| `suggestions` | `ReportSuggestionArray<MessageId>` | const | `[]` | ✗ |
| `variantTypes` | `Set<VariantType>` | const | `new Set<VariantType>()` | ✗ |


---

## Functions

### `traverseTestExpression(node: TestExpression): void`

<details><summary>Code</summary>

```ts
function traverseTestExpression(node: TestExpression): void {
      if (node.test == null) {
        return;
      }
      traverseNode(node.test, true);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Inspects condition of a test expression. (`if`, `while`, `for`, etc.)
     */
```

- **Parameters**:
  - `node: TestExpression`
- **Return Type**: `void`
- **Calls**:
  - `traverseNode`
### `traverseUnaryLogicalExpression(node: TSESTree.UnaryExpression): void`

<details><summary>Code</summary>

```ts
function traverseUnaryLogicalExpression(
      node: TSESTree.UnaryExpression,
    ): void {
      traverseNode(node.argument, true);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Inspects the argument of a unary logical expression (`!`).
     */
```

- **Parameters**:
  - `node: TSESTree.UnaryExpression`
- **Return Type**: `void`
- **Calls**:
  - `traverseNode`
### `traverseLogicalExpression(node: TSESTree.LogicalExpression, isCondition: boolean): void`

<details><summary>Code</summary>

```ts
function traverseLogicalExpression(
      node: TSESTree.LogicalExpression,
      isCondition = false,
    ): void {
      // left argument is always treated as a condition
      traverseNode(node.left, true);
      // if the logical expression is used for control flow,
      // then its right argument is used for its side effects only
      traverseNode(node.right, isCondition);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Inspects the arguments of a logical expression (`&&`, `||`).
     *
     * If the logical expression is a descendant of a test expression,
     * the `isCondition` flag should be set to true.
     * Otherwise, if the logical expression is there on it's own,
     * it's used for control flow and is not a condition itself.
     */
```

- **Parameters**:
  - `node: TSESTree.LogicalExpression`
  - `isCondition: boolean`
- **Return Type**: `void`
- **Calls**:
  - `traverseNode`
- **Internal Comments**:
```
// left argument is always treated as a condition (x3)
// if the logical expression is used for control flow, (x3)
// then its right argument is used for its side effects only (x3)
```

### `traverseCallExpression(node: TSESTree.CallExpression): void`

<details><summary>Code</summary>

```ts
function traverseCallExpression(node: TSESTree.CallExpression): void {
      const assertedArgument = findTruthinessAssertedArgument(services, node);
      if (assertedArgument != null) {
        traverseNode(assertedArgument, true);
      }
      if (isArrayMethodCallWithPredicate(context, services, node)) {
        const predicate = node.arguments.at(0);

        if (predicate) {
          checkArrayMethodCallPredicate(predicate);
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
  - `traverseNode`
  - `isArrayMethodCallWithPredicate (from ../util)`
  - `node.arguments.at`
  - `checkArrayMethodCallPredicate`
### `checkArrayMethodCallPredicate(predicateNode: TSESTree.CallExpressionArgument): void`

<details><summary>Code</summary>

```ts
function checkArrayMethodCallPredicate(
      predicateNode: TSESTree.CallExpressionArgument,
    ): void {
      const isFunctionExpression = ASTUtils.isFunction(predicateNode);

      // custom message for accidental `async` function expressions
      if (isFunctionExpression && predicateNode.async) {
        return context.report({
          node: predicateNode,
          messageId: 'predicateCannotBeAsync',
        });
      }

      const returnTypes = services
        .getTypeAtLocation(predicateNode)
        .getCallSignatures()
        .map(signature => {
          const type = signature.getReturnType();

          if (tsutils.isTypeParameter(type)) {
            return checker.getBaseConstraintOfType(type) ?? type;
          }

          return type;
        });
      const flattenTypes = [
        ...new Set(
          returnTypes.flatMap(type => tsutils.unionConstituents(type)),
        ),
      ];
      const types = inspectVariantTypes(flattenTypes);
      const reportType = determineReportType(types);

      if (reportType == null) {
        return;
      }

      const suggestions: ReportSuggestionArray<MessageId> = [];
      if (
        isFunctionExpression &&
        predicateNode.body.type !== AST_NODE_TYPES.BlockStatement
      ) {
        suggestions.push(
          ...getSuggestionsForConditionError(predicateNode.body, reportType),
        );
      }

      if (isFunctionExpression && !predicateNode.returnType) {
        suggestions.push({
          messageId: 'explicitBooleanReturnType',
          fix: fixer => {
            if (
              predicateNode.type === AST_NODE_TYPES.ArrowFunctionExpression &&
              isParenlessArrowFunction(predicateNode, context.sourceCode)
            ) {
              return [
                fixer.insertTextBefore(predicateNode.params[0], '('),
                fixer.insertTextAfter(predicateNode.params[0], '): boolean'),
              ];
            }

            if (predicateNode.params.length === 0) {
              const closingBracket = nullThrows(
                context.sourceCode.getFirstToken(
                  predicateNode,
                  token => token.value === ')',
                ),
                'function expression has to have a closing parenthesis.',
              );

              return fixer.insertTextAfter(closingBracket, ': boolean');
            }

            const lastClosingParenthesis = nullThrows(
              context.sourceCode.getTokenAfter(
                predicateNode.params[predicateNode.params.length - 1],
                token => token.value === ')',
              ),
              'function expression has to have a closing parenthesis.',
            );

            return fixer.insertTextAfter(lastClosingParenthesis, ': boolean');
          },
        });
      }

      return context.report({
        node: predicateNode,
        messageId: reportType,
        data: {
          context: 'array predicate return type',
        },
        suggest: suggestions,
      });
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Dedicated function to check array method predicate calls. Reports predicate
     * arguments that don't return a boolean value.
     */
```

- **Parameters**:
  - `predicateNode: TSESTree.CallExpressionArgument`
- **Return Type**: `void`
- **Calls**:
  - `ASTUtils.isFunction`
  - `context.report`
  - `services
        .getTypeAtLocation(predicateNode)
        .getCallSignatures()
        .map`
  - `signature.getReturnType`
  - `tsutils.isTypeParameter`
  - `checker.getBaseConstraintOfType`
  - `returnTypes.flatMap`
  - `tsutils.unionConstituents`
  - `inspectVariantTypes`
  - `determineReportType`
  - `suggestions.push`
  - `getSuggestionsForConditionError`
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `context.sourceCode.getTokenAfter`
- **Internal Comments**:
```
// custom message for accidental `async` function expressions
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
            if (
              predicateNode.type === AST_NODE_TYPES.ArrowFunctionExpression &&
              isParenlessArrowFunction(predicateNode, context.sourceCode)
            ) {
              return [
                fixer.insertTextBefore(predicateNode.params[0], '('),
                fixer.insertTextAfter(predicateNode.params[0], '): boolean'),
              ];
            }

            if (predicateNode.params.length === 0) {
              const closingBracket = nullThrows(
                context.sourceCode.getFirstToken(
                  predicateNode,
                  token => token.value === ')',
                ),
                'function expression has to have a closing parenthesis.',
              );

              return fixer.insertTextAfter(closingBracket, ': boolean');
            }

            const lastClosingParenthesis = nullThrows(
              context.sourceCode.getTokenAfter(
                predicateNode.params[predicateNode.params.length - 1],
                token => token.value === ')',
              ),
              'function expression has to have a closing parenthesis.',
            );

            return fixer.insertTextAfter(lastClosingParenthesis, ': boolean');
          }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `context.sourceCode.getTokenAfter`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
            if (
              predicateNode.type === AST_NODE_TYPES.ArrowFunctionExpression &&
              isParenlessArrowFunction(predicateNode, context.sourceCode)
            ) {
              return [
                fixer.insertTextBefore(predicateNode.params[0], '('),
                fixer.insertTextAfter(predicateNode.params[0], '): boolean'),
              ];
            }

            if (predicateNode.params.length === 0) {
              const closingBracket = nullThrows(
                context.sourceCode.getFirstToken(
                  predicateNode,
                  token => token.value === ')',
                ),
                'function expression has to have a closing parenthesis.',
              );

              return fixer.insertTextAfter(closingBracket, ': boolean');
            }

            const lastClosingParenthesis = nullThrows(
              context.sourceCode.getTokenAfter(
                predicateNode.params[predicateNode.params.length - 1],
                token => token.value === ')',
              ),
              'function expression has to have a closing parenthesis.',
            );

            return fixer.insertTextAfter(lastClosingParenthesis, ': boolean');
          }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `context.sourceCode.getTokenAfter`
### `traverseNode(node: TSESTree.Expression, isCondition: boolean): void`

<details><summary>Code</summary>

```ts
function traverseNode(
      node: TSESTree.Expression,
      isCondition: boolean,
    ): void {
      // prevent checking the same node multiple times
      if (traversedNodes.has(node)) {
        return;
      }
      traversedNodes.add(node);

      // for logical operator, we check its operands
      if (
        node.type === AST_NODE_TYPES.LogicalExpression &&
        node.operator !== '??'
      ) {
        traverseLogicalExpression(node, isCondition);
        return;
      }

      // skip if node is not a condition
      if (!isCondition) {
        return;
      }

      checkNode(node);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Inspects any node.
     *
     * If it's a logical expression then it recursively traverses its arguments.
     * If it's any other kind of node then it's type is finally checked against the rule,
     * unless `isCondition` flag is set to false, in which case
     * it's assumed to be used for side effects only and is skipped.
     */
```

- **Parameters**:
  - `node: TSESTree.Expression`
  - `isCondition: boolean`
- **Return Type**: `void`
- **Calls**:
  - `traversedNodes.has`
  - `traversedNodes.add`
  - `traverseLogicalExpression`
  - `checkNode`
- **Internal Comments**:
```
// prevent checking the same node multiple times
// for logical operator, we check its operands
// skip if node is not a condition
```

### `determineReportType(types: Set<VariantType>): ConditionErrorMessageId | undefined`

<details><summary>Code</summary>

```ts
function determineReportType(
      types: Set<VariantType>,
    ): ConditionErrorMessageId | undefined {
      const is = (...wantedTypes: readonly VariantType[]): boolean =>
        types.size === wantedTypes.length &&
        wantedTypes.every(type => types.has(type));

      // boolean
      if (is('boolean') || is('truthy boolean')) {
        // boolean is always ok
        return undefined;
      }

      // never
      if (is('never')) {
        // never is always okay
        return undefined;
      }

      // nullish
      if (is('nullish')) {
        // condition is always false
        return 'conditionErrorNullish';
      }

      // Known edge case: boolean `true` and nullish values are always valid boolean expressions
      if (is('nullish', 'truthy boolean')) {
        return;
      }

      // nullable boolean
      if (is('nullish', 'boolean')) {
        return !options.allowNullableBoolean
          ? 'conditionErrorNullableBoolean'
          : undefined;
      }

      // Known edge case: truthy primitives and nullish values are always valid boolean expressions
      if (
        (options.allowNumber && is('nullish', 'truthy number')) ||
        (options.allowString && is('nullish', 'truthy string'))
      ) {
        return;
      }

      // string
      if (is('string') || is('truthy string')) {
        return !options.allowString ? 'conditionErrorString' : undefined;
      }

      // nullable string
      if (is('nullish', 'string')) {
        return !options.allowNullableString
          ? 'conditionErrorNullableString'
          : undefined;
      }

      // number
      if (is('number') || is('truthy number')) {
        return !options.allowNumber ? 'conditionErrorNumber' : undefined;
      }

      // nullable number
      if (is('nullish', 'number')) {
        return !options.allowNullableNumber
          ? 'conditionErrorNullableNumber'
          : undefined;
      }

      // object
      if (is('object')) {
        return 'conditionErrorObject';
      }

      // nullable object
      if (is('nullish', 'object')) {
        return !options.allowNullableObject
          ? 'conditionErrorNullableObject'
          : undefined;
      }

      // nullable enum
      if (
        is('nullish', 'number', 'enum') ||
        is('nullish', 'string', 'enum') ||
        is('nullish', 'truthy number', 'enum') ||
        is('nullish', 'truthy string', 'enum') ||
        // mixed enums
        is('nullish', 'truthy number', 'truthy string', 'enum') ||
        is('nullish', 'truthy number', 'string', 'enum') ||
        is('nullish', 'truthy string', 'number', 'enum') ||
        is('nullish', 'number', 'string', 'enum')
      ) {
        return !options.allowNullableEnum
          ? 'conditionErrorNullableEnum'
          : undefined;
      }

      // any
      if (is('any')) {
        return !options.allowAny ? 'conditionErrorAny' : undefined;
      }

      return 'conditionErrorOther';
    }
```
</details>

- **Parameters**:
  - `types: Set<VariantType>`
- **Return Type**: `ConditionErrorMessageId | undefined`
- **Calls**:
  - `wantedTypes.every`
  - `types.has`
  - `is`
- **Internal Comments**:
```
// boolean
// boolean is always ok
// never
// never is always okay
// nullish
// condition is always false
// Known edge case: boolean `true` and nullish values are always valid boolean expressions
// nullable boolean
// Known edge case: truthy primitives and nullish values are always valid boolean expressions
// string
// nullable string
// number
// nullable number
// object
// nullable object
// nullable enum
// mixed enums (x2)
// any
```

### `is(wantedTypes: readonly VariantType[]): boolean`

<details><summary>Code</summary>

```ts
(...wantedTypes: readonly VariantType[]): boolean =>
        types.size === wantedTypes.length &&
        wantedTypes.every(type => types.has(type))
```
</details>

- **Parameters**:
  - `wantedTypes: readonly VariantType[]`
- **Return Type**: `boolean`
### `getSuggestionsForConditionError(node: TSESTree.Expression, conditionError: ConditionErrorMessageId): ReportSuggestionArray<MessageId>`

<details><summary>Code</summary>

```ts
function getSuggestionsForConditionError(
      node: TSESTree.Expression,
      conditionError: ConditionErrorMessageId,
    ): ReportSuggestionArray<MessageId> {
      switch (conditionError) {
        case 'conditionErrorAny':
          return [
            {
              messageId: 'conditionFixCastBoolean',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `Boolean(${code})`,
              }),
            },
          ];
        case 'conditionErrorNullableBoolean':
          if (isLogicalNegationExpression(node.parent)) {
            // if (!nullableBoolean)
            return [
              {
                messageId: 'conditionFixDefaultFalse',
                fix: getWrappingFixer({
                  node,
                  sourceCode: context.sourceCode,
                  wrap: code => `${code} ?? false`,
                }),
              },
              {
                messageId: 'conditionFixCompareFalse',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  wrap: code => `${code} === false`,
                }),
              },
            ];
          }
          // if (nullableBoolean)
          return [
            {
              messageId: 'conditionFixDefaultFalse',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `${code} ?? false`,
              }),
            },
            {
              messageId: 'conditionFixCompareTrue',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `${code} === true`,
              }),
            },
          ];

        case 'conditionErrorNullableEnum':
          if (isLogicalNegationExpression(node.parent)) {
            return [
              {
                messageId: 'conditionFixCompareNullish',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  wrap: code => `${code} == null`,
                }),
              },
            ];
          }
          return [
            {
              messageId: 'conditionFixCompareNullish',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `${code} != null`,
              }),
            },
          ];

        case 'conditionErrorNullableNumber':
          if (isLogicalNegationExpression(node.parent)) {
            // if (!nullableNumber)
            return [
              {
                messageId: 'conditionFixCompareNullish',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  wrap: code => `${code} == null`,
                }),
              },
              {
                messageId: 'conditionFixDefaultZero',
                fix: getWrappingFixer({
                  node,
                  sourceCode: context.sourceCode,
                  wrap: code => `${code} ?? 0`,
                }),
              },
              {
                messageId: 'conditionFixCastBoolean',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  wrap: code => `!Boolean(${code})`,
                }),
              },
            ];
          }
          // if (nullableNumber)
          return [
            {
              messageId: 'conditionFixCompareNullish',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `${code} != null`,
              }),
            },
            {
              messageId: 'conditionFixDefaultZero',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `${code} ?? 0`,
              }),
            },
            {
              messageId: 'conditionFixCastBoolean',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `Boolean(${code})`,
              }),
            },
          ];

        case 'conditionErrorNullableObject':
          if (isLogicalNegationExpression(node.parent)) {
            // if (!nullableObject)
            return [
              {
                messageId: 'conditionFixCompareNullish',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  wrap: code => `${code} == null`,
                }),
              },
            ];
          }
          // if (nullableObject)
          return [
            {
              messageId: 'conditionFixCompareNullish',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `${code} != null`,
              }),
            },
          ];

        case 'conditionErrorNullableString':
          if (isLogicalNegationExpression(node.parent)) {
            // if (!nullableString)
            return [
              {
                messageId: 'conditionFixCompareNullish',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  wrap: code => `${code} == null`,
                }),
              },
              {
                messageId: 'conditionFixDefaultEmptyString',
                fix: getWrappingFixer({
                  node,
                  sourceCode: context.sourceCode,
                  wrap: code => `${code} ?? ""`,
                }),
              },
              {
                messageId: 'conditionFixCastBoolean',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  wrap: code => `!Boolean(${code})`,
                }),
              },
            ];
          }
          // if (nullableString)
          return [
            {
              messageId: 'conditionFixCompareNullish',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `${code} != null`,
              }),
            },
            {
              messageId: 'conditionFixDefaultEmptyString',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `${code} ?? ""`,
              }),
            },
            {
              messageId: 'conditionFixCastBoolean',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `Boolean(${code})`,
              }),
            },
          ];

        case 'conditionErrorNumber':
          if (isArrayLengthExpression(node, checker, services)) {
            if (isLogicalNegationExpression(node.parent)) {
              // if (!array.length)
              return [
                {
                  messageId: 'conditionFixCompareArrayLengthZero',
                  fix: getWrappingFixer({
                    node: node.parent,
                    innerNode: node,
                    sourceCode: context.sourceCode,
                    wrap: code => `${code} === 0`,
                  }),
                },
              ];
            }
            // if (array.length)
            return [
              {
                messageId: 'conditionFixCompareArrayLengthNonzero',
                fix: getWrappingFixer({
                  node,
                  sourceCode: context.sourceCode,
                  wrap: code => `${code} > 0`,
                }),
              },
            ];
          }
          if (isLogicalNegationExpression(node.parent)) {
            // if (!number)
            return [
              {
                messageId: 'conditionFixCompareZero',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  // TODO: we have to compare to 0n if the type is bigint
                  wrap: code => `${code} === 0`,
                }),
              },
              {
                // TODO: don't suggest this for bigint because it can't be NaN
                messageId: 'conditionFixCompareNaN',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  wrap: code => `Number.isNaN(${code})`,
                }),
              },
              {
                messageId: 'conditionFixCastBoolean',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  wrap: code => `!Boolean(${code})`,
                }),
              },
            ];
          }
          // if (number)
          return [
            {
              messageId: 'conditionFixCompareZero',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `${code} !== 0`,
              }),
            },
            {
              messageId: 'conditionFixCompareNaN',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `!Number.isNaN(${code})`,
              }),
            },
            {
              messageId: 'conditionFixCastBoolean',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `Boolean(${code})`,
              }),
            },
          ];

        case 'conditionErrorString':
          if (isLogicalNegationExpression(node.parent)) {
            // if (!string)
            return [
              {
                messageId: 'conditionFixCompareStringLength',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  wrap: code => `${code}.length === 0`,
                }),
              },
              {
                messageId: 'conditionFixCompareEmptyString',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  wrap: code => `${code} === ""`,
                }),
              },
              {
                messageId: 'conditionFixCastBoolean',
                fix: getWrappingFixer({
                  node: node.parent,
                  innerNode: node,
                  sourceCode: context.sourceCode,
                  wrap: code => `!Boolean(${code})`,
                }),
              },
            ];
          }
          // if (string)
          return [
            {
              messageId: 'conditionFixCompareStringLength',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `${code}.length > 0`,
              }),
            },
            {
              messageId: 'conditionFixCompareEmptyString',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `${code} !== ""`,
              }),
            },
            {
              messageId: 'conditionFixCastBoolean',
              fix: getWrappingFixer({
                node,
                sourceCode: context.sourceCode,
                wrap: code => `Boolean(${code})`,
              }),
            },
          ];

        case 'conditionErrorObject':
        case 'conditionErrorNullish':
        case 'conditionErrorOther':
          return [];
        default:
          conditionError satisfies never;
          throw new Error('Unreachable');
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
  - `conditionError: ConditionErrorMessageId`
- **Return Type**: `ReportSuggestionArray<MessageId>`
- **Calls**:
  - `getWrappingFixer (from ../util)`
  - `isLogicalNegationExpression`
  - `isArrayLengthExpression`
- **Internal Comments**:
```
// if (!nullableBoolean)
// if (nullableBoolean)
// if (!nullableNumber)
// if (nullableNumber)
// if (!nullableObject)
// if (nullableObject)
// if (!nullableString)
// if (nullableString)
// if (!array.length)
// if (array.length)
// if (!number)
// TODO: we have to compare to 0n if the type is bigint (x2)
// TODO: don't suggest this for bigint because it can't be NaN (x2)
// if (number)
// if (!string)
// if (string)
```

### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === true`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === true`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === true`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === true`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `checkNode(node: TSESTree.Expression): void`

<details><summary>Code</summary>

```ts
function checkNode(node: TSESTree.Expression): void {
      const type = getConstrainedTypeAtLocation(services, node);
      const types = inspectVariantTypes(tsutils.unionConstituents(type));
      const reportType = determineReportType(types);

      if (reportType != null) {
        context.report({
          node,
          messageId: reportType,
          data: {
            context: 'conditional',
          },
          suggest: getSuggestionsForConditionError(node, reportType),
        });
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * This function does the actual type check on a node.
     * It analyzes the type of a node and checks if it is allowed in a boolean context.
     */
```

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `void`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `inspectVariantTypes`
  - `tsutils.unionConstituents`
  - `determineReportType`
  - `context.report`
  - `getSuggestionsForConditionError`
### `inspectVariantTypes(types: ts.Type[]): Set<VariantType>`

<details><summary>Code</summary>

```ts
function inspectVariantTypes(types: ts.Type[]): Set<VariantType> {
      const variantTypes = new Set<VariantType>();

      if (
        types.some(type =>
          tsutils.isTypeFlagSet(
            type,
            ts.TypeFlags.Null | ts.TypeFlags.Undefined | ts.TypeFlags.VoidLike,
          ),
        )
      ) {
        variantTypes.add('nullish');
      }
      const booleans = types.filter(type =>
        tsutils.isTypeFlagSet(type, ts.TypeFlags.BooleanLike),
      );

      // If incoming type is either "true" or "false", there will be one type
      // object with intrinsicName set accordingly
      // If incoming type is boolean, there will be two type objects with
      // intrinsicName set "true" and "false" each because of ts-api-utils.unionConstituents()
      if (booleans.length === 1) {
        variantTypes.add(
          tsutils.isTrueLiteralType(booleans[0]) ? 'truthy boolean' : 'boolean',
        );
      } else if (booleans.length === 2) {
        variantTypes.add('boolean');
      }

      const strings = types.filter(type =>
        tsutils.isTypeFlagSet(type, ts.TypeFlags.StringLike),
      );

      if (strings.length) {
        if (
          strings.every(type => type.isStringLiteral() && type.value !== '')
        ) {
          variantTypes.add('truthy string');
        } else {
          variantTypes.add('string');
        }
      }

      const numbers = types.filter(type =>
        tsutils.isTypeFlagSet(
          type,
          ts.TypeFlags.NumberLike | ts.TypeFlags.BigIntLike,
        ),
      );

      if (numbers.length) {
        if (numbers.every(type => type.isNumberLiteral() && type.value !== 0)) {
          variantTypes.add('truthy number');
        } else {
          variantTypes.add('number');
        }
      }

      if (
        types.some(type => tsutils.isTypeFlagSet(type, ts.TypeFlags.EnumLike))
      ) {
        variantTypes.add('enum');
      }

      if (
        types.some(
          type =>
            !tsutils.isTypeFlagSet(
              type,
              ts.TypeFlags.Null |
                ts.TypeFlags.Undefined |
                ts.TypeFlags.VoidLike |
                ts.TypeFlags.BooleanLike |
                ts.TypeFlags.StringLike |
                ts.TypeFlags.NumberLike |
                ts.TypeFlags.BigIntLike |
                ts.TypeFlags.TypeParameter |
                ts.TypeFlags.Any |
                ts.TypeFlags.Unknown |
                ts.TypeFlags.Never,
            ),
        )
      ) {
        variantTypes.add(types.some(isBrandedBoolean) ? 'boolean' : 'object');
      }

      if (
        types.some(type =>
          tsutils.isTypeFlagSet(
            type,
            ts.TypeFlags.TypeParameter |
              ts.TypeFlags.Any |
              ts.TypeFlags.Unknown,
          ),
        )
      ) {
        variantTypes.add('any');
      }

      if (types.some(type => tsutils.isTypeFlagSet(type, ts.TypeFlags.Never))) {
        variantTypes.add('never');
      }

      return variantTypes;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check union variants for the types we care about
     */
```

- **Parameters**:
  - `types: ts.Type[]`
- **Return Type**: `Set<VariantType>`
- **Calls**:
  - `types.some`
  - `tsutils.isTypeFlagSet`
  - `variantTypes.add`
  - `types.filter`
  - `tsutils.isTrueLiteralType`
  - `strings.every`
  - `type.isStringLiteral`
  - `numbers.every`
  - `type.isNumberLiteral`
- **Internal Comments**:
```
// If incoming type is either "true" or "false", there will be one type
// object with intrinsicName set accordingly
// If incoming type is boolean, there will be two type objects with
// intrinsicName set "true" and "false" each because of ts-api-utils.unionConstituents()
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
            if (
              predicateNode.type === AST_NODE_TYPES.ArrowFunctionExpression &&
              isParenlessArrowFunction(predicateNode, context.sourceCode)
            ) {
              return [
                fixer.insertTextBefore(predicateNode.params[0], '('),
                fixer.insertTextAfter(predicateNode.params[0], '): boolean'),
              ];
            }

            if (predicateNode.params.length === 0) {
              const closingBracket = nullThrows(
                context.sourceCode.getFirstToken(
                  predicateNode,
                  token => token.value === ')',
                ),
                'function expression has to have a closing parenthesis.',
              );

              return fixer.insertTextAfter(closingBracket, ': boolean');
            }

            const lastClosingParenthesis = nullThrows(
              context.sourceCode.getTokenAfter(
                predicateNode.params[predicateNode.params.length - 1],
                token => token.value === ')',
              ),
              'function expression has to have a closing parenthesis.',
            );

            return fixer.insertTextAfter(lastClosingParenthesis, ': boolean');
          }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `context.sourceCode.getTokenAfter`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
            if (
              predicateNode.type === AST_NODE_TYPES.ArrowFunctionExpression &&
              isParenlessArrowFunction(predicateNode, context.sourceCode)
            ) {
              return [
                fixer.insertTextBefore(predicateNode.params[0], '('),
                fixer.insertTextAfter(predicateNode.params[0], '): boolean'),
              ];
            }

            if (predicateNode.params.length === 0) {
              const closingBracket = nullThrows(
                context.sourceCode.getFirstToken(
                  predicateNode,
                  token => token.value === ')',
                ),
                'function expression has to have a closing parenthesis.',
              );

              return fixer.insertTextAfter(closingBracket, ': boolean');
            }

            const lastClosingParenthesis = nullThrows(
              context.sourceCode.getTokenAfter(
                predicateNode.params[predicateNode.params.length - 1],
                token => token.value === ')',
              ),
              'function expression has to have a closing parenthesis.',
            );

            return fixer.insertTextAfter(lastClosingParenthesis, ': boolean');
          }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `context.sourceCode.getTokenAfter`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? false`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === true`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === true`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === true`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === true`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} == null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} != null`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} ?? ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Number.isNaN(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length === 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} === ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `!Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code}.length > 0`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `${code} !== ""`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Boolean(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `isLogicalNegationExpression(node: TSESTree.Node): node is TSESTree.UnaryExpression`

<details><summary>Code</summary>

```ts
function isLogicalNegationExpression(
  node: TSESTree.Node,
): node is TSESTree.UnaryExpression {
  return node.type === AST_NODE_TYPES.UnaryExpression && node.operator === '!';
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.UnaryExpression`
### `isArrayLengthExpression(node: TSESTree.Node, typeChecker: ts.TypeChecker, services: ParserServicesWithTypeInformation): node is TSESTree.MemberExpressionNonComputedName`

<details><summary>Code</summary>

```ts
function isArrayLengthExpression(
  node: TSESTree.Node,
  typeChecker: ts.TypeChecker,
  services: ParserServicesWithTypeInformation,
): node is TSESTree.MemberExpressionNonComputedName {
  if (node.type !== AST_NODE_TYPES.MemberExpression) {
    return false;
  }
  if (node.computed) {
    return false;
  }
  if (node.property.name !== 'length') {
    return false;
  }
  const objectType = getConstrainedTypeAtLocation(services, node.object);
  return isTypeArrayTypeOrUnionOfArrayTypes(objectType, typeChecker);
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `typeChecker: ts.TypeChecker`
  - `services: ParserServicesWithTypeInformation`
- **Return Type**: `node is TSESTree.MemberExpressionNonComputedName`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `isTypeArrayTypeOrUnionOfArrayTypes (from ../util)`
### `isBrandedBoolean(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isBrandedBoolean(type: ts.Type): boolean {
  return (
    type.isIntersection() &&
    type.types.some(childType => isBooleanType(childType))
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Verify is the type is a branded boolean (e.g. `type Foo = boolean & { __brand: 'Foo' }`)
 *
 * @param type The type checked
 */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `type.isIntersection`
  - `type.types.some`
  - `isBooleanType`
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

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    allowAny?: boolean;
    allowNullableBoolean?: boolean;
    allowNullableEnum?: boolean;
    allowNullableNumber?: boolean;
    allowNullableObject?: boolean;
    allowNullableString?: boolean;
    allowNumber?: boolean;
    allowRuleToRunWithoutStrictNullChecksIKnowWhatIAmDoing?: boolean;
    allowString?: boolean;
  },
];
```

### `ConditionErrorMessageId`

```ts
type ConditionErrorMessageId = | 'conditionErrorAny'
  | 'conditionErrorNullableBoolean'
  | 'conditionErrorNullableEnum'
  | 'conditionErrorNullableNumber'
  | 'conditionErrorNullableObject'
  | 'conditionErrorNullableString'
  | 'conditionErrorNullish'
  | 'conditionErrorNumber'
  | 'conditionErrorObject'
  | 'conditionErrorOther'
  | 'conditionErrorString';
```

### `MessageId`

```ts
type MessageId = | 'conditionFixCastBoolean'
  | 'conditionFixCompareArrayLengthNonzero'
  | 'conditionFixCompareArrayLengthZero'
  | 'conditionFixCompareEmptyString'
  | 'conditionFixCompareFalse'
  | 'conditionFixCompareNaN'
  | 'conditionFixCompareNullish'
  | 'conditionFixCompareStringLength'
  | 'conditionFixCompareTrue'
  | 'conditionFixCompareZero'
  | 'conditionFixDefaultEmptyString'
  | 'conditionFixDefaultFalse'
  | 'conditionFixDefaultZero'
  | 'explicitBooleanReturnType'
  | 'noStrictNullCheck'
  | 'predicateCannotBeAsync'
  | ConditionErrorMessageId;
```

### `TestExpression`

```ts
type TestExpression = | TSESTree.ConditionalExpression
      | TSESTree.DoWhileStatement
      | TSESTree.ForStatement
      | TSESTree.IfStatement
      | TSESTree.WhileStatement;
```

### `VariantType`

/** The types we care about */

```ts
type VariantType = | 'any'
      | 'boolean'
      | 'enum'
      | 'never'
      | 'nullish'
      | 'number'
      | 'object'
      | 'string'
      | 'truthy boolean'
      | 'truthy number'
      | 'truthy string';
```


---