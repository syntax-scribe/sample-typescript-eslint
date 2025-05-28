[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `analyzeChain.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 9 |
| 🧱 Classes | 0 |
| 📦 Imports | 23 |
| 📊 Variables & Constants | 13 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-optional-chain-utils/analyzeChain.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserServicesWithTypeInformation` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `ReportDescriptor` | `@typescript-eslint/utils/ts-eslint` |
| `ReportFixFunction` | `@typescript-eslint/utils/ts-eslint` |
| `RuleContext` | `@typescript-eslint/utils/ts-eslint` |
| `SourceCode` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `unionConstituents` | `ts-api-utils` |
| `ValidOperand` | `./gatherLogicalOperands` |
| `PreferOptionalChainMessageIds` | `./PreferOptionalChainOptions` |
| `PreferOptionalChainOptions` | `./PreferOptionalChainOptions` |
| `getFixOrSuggest` | `../../util` |
| `getOperatorPrecedenceForNode` | `../../util` |
| `isClosingParenToken` | `../../util` |
| `isOpeningParenToken` | `../../util` |
| `isTypeFlagSet` | `../../util` |
| `nullThrows` | `../../util` |
| `NullThrowsReasons` | `../../util` |
| `OperatorPrecedence` | `../../util` |
| `checkNullishAndReport` | `./checkNullishAndReport` |
| `compareNodes` | `./compareNodes` |
| `NodeComparisonResult` | `./compareNodes` |
| `NullishComparisonType` | `./gatherLogicalOperands` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `typeFlag` | `number` | const | `typeFlagIn | ts.TypeFlags.Any | ts.TypeFlags.Unknown` | ✗ |
| `leftNode` | `TSESTree.Expression` | const | `chain[0].node` | ✗ |
| `rightNode` | `TSESTree.Expression` | const | `chain[chain.length - 1].node` | ✗ |
| `lastOperand` | `ValidOperand` | const | `chain[chain.length - 1]` | ✗ |
| `useSuggestionFixer` | `boolean` | let/var | `*not shown*` | ✗ |
| `parts` | `any[]` | const | `[]` | ✗ |
| `str` | `string` | let/var | `''` | ✗ |
| `operator` | `any` | const | `lastOperand.node.operator` | ✗ |
| `unaryOperator` | `string` | const | `lastOperand.node.right.type === AST_NODE_TYPES.UnaryExpression
            ? `${lastOperand.node.right.operator} `
            : ''` | ✗ |
| `unaryOperator` | `string` | const | `lastOperand.node.left.type === AST_NODE_TYPES.UnaryExpression
          ? `${lastOperand.node.left.operator} `
          : ''` | ✗ |
| `subChain` | `(readonly ValidOperand[] | ValidOperand)[]` | let/var | `[]` | ✗ |
| `operand` | `ValidOperand` | const | `chain[i]` | ✗ |
| `currentOperand` | `ValidOperand` | const | `validatedOperands[0]` | ✗ |


---

## Functions

### `includesType(parserServices: ParserServicesWithTypeInformation, node: TSESTree.Node, typeFlagIn: ts.TypeFlags): boolean`

<details><summary>Code</summary>

```ts
function includesType(
  parserServices: ParserServicesWithTypeInformation,
  node: TSESTree.Node,
  typeFlagIn: ts.TypeFlags,
): boolean {
  const typeFlag = typeFlagIn | ts.TypeFlags.Any | ts.TypeFlags.Unknown;
  const types = unionConstituents(parserServices.getTypeAtLocation(node));
  for (const type of types) {
    if (isTypeFlagSet(type, typeFlag)) {
      return true;
    }
  }
  return false;
}
```
</details>

- **Parameters**:
  - `parserServices: ParserServicesWithTypeInformation`
  - `node: TSESTree.Node`
  - `typeFlagIn: ts.TypeFlags`
- **Return Type**: `boolean`
- **Calls**:
  - `unionConstituents (from ts-api-utils)`
  - `parserServices.getTypeAtLocation`
  - `isTypeFlagSet (from ../../util)`
### `analyzeAndChainOperand(parserServices: ParserServicesWithTypeInformation, operand: ValidOperand, index: number, chain: readonly ValidOperand[]): [ValidOperand] | [ValidOperand, ValidOperand]`

<details><summary>Code</summary>

```ts
(
  parserServices,
  operand,
  index,
  chain,
) => {
  switch (operand.comparisonType) {
    case NullishComparisonType.Boolean: {
      const nextOperand = chain.at(index + 1);
      if (
        nextOperand?.comparisonType ===
          NullishComparisonType.NotStrictEqualNull &&
        operand.comparedName.type === AST_NODE_TYPES.Identifier
      ) {
        return null;
      }
      return [operand];
    }

    case NullishComparisonType.NotEqualNullOrUndefined:
      return [operand];

    case NullishComparisonType.NotStrictEqualNull: {
      // handle `x !== null && x !== undefined`
      const nextOperand = chain.at(index + 1);
      if (
        nextOperand?.comparisonType ===
          NullishComparisonType.NotStrictEqualUndefined &&
        compareNodes(operand.comparedName, nextOperand.comparedName) ===
          NodeComparisonResult.Equal
      ) {
        return [operand, nextOperand];
      }
      if (
        includesType(
          parserServices,
          operand.comparedName,
          ts.TypeFlags.Undefined,
        )
      ) {
        // we know the next operand is not an `undefined` check and that this
        // operand includes `undefined` - which means that making this an
        // optional chain would change the runtime behavior of the expression
        return null;
      }

      return [operand];
    }

    case NullishComparisonType.NotStrictEqualUndefined: {
      // handle `x !== undefined && x !== null`
      const nextOperand = chain.at(index + 1);
      if (
        nextOperand?.comparisonType ===
          NullishComparisonType.NotStrictEqualNull &&
        compareNodes(operand.comparedName, nextOperand.comparedName) ===
          NodeComparisonResult.Equal
      ) {
        return [operand, nextOperand];
      }
      if (
        includesType(parserServices, operand.comparedName, ts.TypeFlags.Null)
      ) {
        // we know the next operand is not a `null` check and that this
        // operand includes `null` - which means that making this an
        // optional chain would change the runtime behavior of the expression
        return null;
      }

      return [operand];
    }

    default:
      return null;
  }
}
```
</details>

- **Parameters**:
  - `parserServices: ParserServicesWithTypeInformation`
  - `operand: ValidOperand`
  - `index: number`
  - `chain: readonly ValidOperand[]`
- **Return Type**: `[ValidOperand] | [ValidOperand, ValidOperand]`
- **Calls**:
  - `chain.at`
  - `compareNodes (from ./compareNodes)`
  - `includesType`
- **Internal Comments**:
```
// handle `x !== null && x !== undefined` (x2)
// we know the next operand is not an `undefined` check and that this
// operand includes `undefined` - which means that making this an
// optional chain would change the runtime behavior of the expression (x2)
// handle `x !== undefined && x !== null` (x2)
// we know the next operand is not a `null` check and that this
// operand includes `null` - which means that making this an
```

### `analyzeOrChainOperand(parserServices: ParserServicesWithTypeInformation, operand: ValidOperand, index: number, chain: readonly ValidOperand[]): [ValidOperand] | [ValidOperand, ValidOperand]`

<details><summary>Code</summary>

```ts
(
  parserServices,
  operand,
  index,
  chain,
) => {
  switch (operand.comparisonType) {
    case NullishComparisonType.NotBoolean:
    case NullishComparisonType.EqualNullOrUndefined:
      return [operand];

    case NullishComparisonType.StrictEqualNull: {
      // handle `x === null || x === undefined`
      const nextOperand = chain.at(index + 1);
      if (
        nextOperand?.comparisonType ===
          NullishComparisonType.StrictEqualUndefined &&
        compareNodes(operand.comparedName, nextOperand.comparedName) ===
          NodeComparisonResult.Equal
      ) {
        return [operand, nextOperand];
      }
      if (
        includesType(
          parserServices,
          operand.comparedName,
          ts.TypeFlags.Undefined,
        )
      ) {
        // we know the next operand is not an `undefined` check and that this
        // operand includes `undefined` - which means that making this an
        // optional chain would change the runtime behavior of the expression
        return null;
      }

      return [operand];
    }

    case NullishComparisonType.StrictEqualUndefined: {
      // handle `x === undefined || x === null`
      const nextOperand = chain.at(index + 1);
      if (
        nextOperand?.comparisonType === NullishComparisonType.StrictEqualNull &&
        compareNodes(operand.comparedName, nextOperand.comparedName) ===
          NodeComparisonResult.Equal
      ) {
        return [operand, nextOperand];
      }
      if (
        includesType(parserServices, operand.comparedName, ts.TypeFlags.Null)
      ) {
        // we know the next operand is not a `null` check and that this
        // operand includes `null` - which means that making this an
        // optional chain would change the runtime behavior of the expression
        return null;
      }

      return [operand];
    }

    default:
      return null;
  }
}
```
</details>

- **Parameters**:
  - `parserServices: ParserServicesWithTypeInformation`
  - `operand: ValidOperand`
  - `index: number`
  - `chain: readonly ValidOperand[]`
- **Return Type**: `[ValidOperand] | [ValidOperand, ValidOperand]`
- **Calls**:
  - `chain.at`
  - `compareNodes (from ./compareNodes)`
  - `includesType`
- **Internal Comments**:
```
// handle `x === null || x === undefined` (x2)
// we know the next operand is not an `undefined` check and that this
// operand includes `undefined` - which means that making this an
// optional chain would change the runtime behavior of the expression (x2)
// handle `x === undefined || x === null` (x2)
// we know the next operand is not a `null` check and that this
// operand includes `null` - which means that making this an
```

### `getReportRange(chain: ValidOperand[], boundary: TSESTree.Range, sourceCode: SourceCode): TSESTree.Range`

<details><summary>Code</summary>

```ts
function getReportRange(
  chain: ValidOperand[],
  boundary: TSESTree.Range,
  sourceCode: SourceCode,
): TSESTree.Range {
  const leftNode = chain[0].node;
  const rightNode = chain[chain.length - 1].node;
  let leftMost = nullThrows(
    sourceCode.getFirstToken(leftNode),
    NullThrowsReasons.MissingToken('any token', leftNode.type),
  );
  let rightMost = nullThrows(
    sourceCode.getLastToken(rightNode),
    NullThrowsReasons.MissingToken('any token', rightNode.type),
  );

  while (leftMost.range[0] > boundary[0]) {
    const token = sourceCode.getTokenBefore(leftMost);
    if (!token || !isOpeningParenToken(token) || token.range[0] < boundary[0]) {
      break;
    }
    leftMost = token;
  }

  while (rightMost.range[1] < boundary[1]) {
    const token = sourceCode.getTokenAfter(rightMost);
    if (!token || !isClosingParenToken(token) || token.range[1] > boundary[1]) {
      break;
    }
    rightMost = token;
  }

  return [leftMost.range[0], rightMost.range[1]];
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns the range that needs to be reported from the chain.
 * @param chain The chain of logical expressions.
 * @param boundary The boundary range that the range to report cannot fall outside.
 * @param sourceCode The source code to get tokens.
 * @returns The range to report.
 */
```

- **Parameters**:
  - `chain: ValidOperand[]`
  - `boundary: TSESTree.Range`
  - `sourceCode: SourceCode`
- **Return Type**: `TSESTree.Range`
- **Calls**:
  - `nullThrows (from ../../util)`
  - `sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `sourceCode.getLastToken`
  - `sourceCode.getTokenBefore`
  - `isOpeningParenToken (from ../../util)`
  - `sourceCode.getTokenAfter`
  - `isClosingParenToken (from ../../util)`
### `getReportDescriptor(sourceCode: SourceCode, parserServices: ParserServicesWithTypeInformation, node: TSESTree.Node, operator: '&&' | '||', options: PreferOptionalChainOptions, chain: ValidOperand[]): ReportDescriptor<PreferOptionalChainMessageIds>`

<details><summary>Code</summary>

```ts
function getReportDescriptor(
  sourceCode: SourceCode,
  parserServices: ParserServicesWithTypeInformation,
  node: TSESTree.Node,
  operator: '&&' | '||',
  options: PreferOptionalChainOptions,
  chain: ValidOperand[],
): ReportDescriptor<PreferOptionalChainMessageIds> {
  const lastOperand = chain[chain.length - 1];

  let useSuggestionFixer: boolean;
  if (
    options.allowPotentiallyUnsafeFixesThatModifyTheReturnTypeIKnowWhatImDoing ===
    true
  ) {
    // user has opted-in to the unsafe behavior
    useSuggestionFixer = false;
  }
  // optional chain specifically will union `undefined` into the final type
  // so we need to make sure that there is at least one operand that includes
  // `undefined`, or else we're going to change the final type - which is
  // unsafe and might cause downstream type errors.
  else if (
    lastOperand.comparisonType === NullishComparisonType.EqualNullOrUndefined ||
    lastOperand.comparisonType ===
      NullishComparisonType.NotEqualNullOrUndefined ||
    lastOperand.comparisonType === NullishComparisonType.StrictEqualUndefined ||
    lastOperand.comparisonType ===
      NullishComparisonType.NotStrictEqualUndefined ||
    (operator === '||' &&
      lastOperand.comparisonType === NullishComparisonType.NotBoolean)
  ) {
    // we know the last operand is an equality check - so the change in types
    // DOES NOT matter and will not change the runtime result or cause a type
    // check error
    useSuggestionFixer = false;
  } else {
    useSuggestionFixer = true;

    for (const operand of chain) {
      if (includesType(parserServices, operand.node, ts.TypeFlags.Undefined)) {
        useSuggestionFixer = false;
        break;
      }
    }

    // TODO - we could further reduce the false-positive rate of this check by
    //        checking for cases where the change in types don't matter like
    //        the test location of an if/while/etc statement.
    //        but it's quite complex to do this without false-negatives, so
    //        for now we'll just be over-eager with our matching.
    //
    //        it's MUCH better to false-positive here and only provide a
    //        suggestion fixer, rather than false-negative and autofix to
    //        broken code.
  }

  // In its most naive form we could just slap `?.` for every single part of the
  // chain. However this would be undesirable because it'd create unnecessary
  // conditions in the user's code where there were none before - and it would
  // cause errors with rules like our `no-unnecessary-condition`.
  //
  // Instead we want to include the minimum number of `?.` required to correctly
  // unify the code into a single chain. Naively you might think that we can
  // just take the final operand add `?.` after the locations from the previous
  // operands - however this won't be correct either because earlier operands
  // can include a necessary `?.` that's not needed or included in a later
  // operand.
  //
  // So instead what we need to do is to start at the first operand and
  // iteratively diff it against the next operand, and add the difference to the
  // first operand.
  //
  // eg
  // `foo && foo.bar && foo.bar.baz?.bam && foo.bar.baz.bam()`
  // 1) `foo`
  // 2) diff(`foo`, `foo.bar`) = `.bar`
  // 3) result = `foo?.bar`
  // 4) diff(`foo.bar`, `foo.bar.baz?.bam`) = `.baz?.bam`
  // 5) result = `foo?.bar?.baz?.bam`
  // 6) diff(`foo.bar.baz?.bam`, `foo.bar.baz.bam()`) = `()`
  // 7) result = `foo?.bar?.baz?.bam?.()`

  const parts = [];
  for (const current of chain) {
    const nextOperand = flattenChainExpression(
      sourceCode,
      current.comparedName,
    );
    const diff = nextOperand.slice(parts.length);
    if (diff.length > 0) {
      if (parts.length > 0) {
        // we need to make the first operand of the diff optional so it matches the
        // logic before merging
        // foo.bar && foo.bar.baz
        // diff = .baz
        // result = foo.bar?.baz
        diff[0].optional = true;
      }
      parts.push(...diff);
    }
  }

  let newCode = parts
    .map(part => {
      let str = '';
      if (part.optional) {
        str += '?.';
      } else {
        if (part.nonNull) {
          str += '!';
        }
        if (part.requiresDot) {
          str += '.';
        }
      }
      if (
        part.precedence !== OperatorPrecedence.Invalid &&
        part.precedence < OperatorPrecedence.Member
      ) {
        str += `(${part.text})`;
      } else {
        str += part.text;
      }
      return str;
    })
    .join('');

  if (lastOperand.node.type === AST_NODE_TYPES.BinaryExpression) {
    // retain the ending comparison for cases like
    // x && x.a != null
    // x && typeof x.a !== 'undefined'
    const operator = lastOperand.node.operator;
    const { left, right } = (() => {
      if (lastOperand.isYoda) {
        const unaryOperator =
          lastOperand.node.right.type === AST_NODE_TYPES.UnaryExpression
            ? `${lastOperand.node.right.operator} `
            : '';

        return {
          left: sourceCode.getText(lastOperand.node.left),
          right: unaryOperator + newCode,
        };
      }
      const unaryOperator =
        lastOperand.node.left.type === AST_NODE_TYPES.UnaryExpression
          ? `${lastOperand.node.left.operator} `
          : '';
      return {
        left: unaryOperator + newCode,
        right: sourceCode.getText(lastOperand.node.right),
      };
    })();

    newCode = `${left} ${operator} ${right}`;
  } else if (lastOperand.comparisonType === NullishComparisonType.NotBoolean) {
    newCode = `!${newCode}`;
  }

  const reportRange = getReportRange(chain, node.range, sourceCode);

  const fix: ReportFixFunction = fixer =>
    fixer.replaceTextRange(reportRange, newCode);

  return {
    loc: {
      end: sourceCode.getLocFromIndex(reportRange[1]),
      start: sourceCode.getLocFromIndex(reportRange[0]),
    },
    messageId: 'preferOptionalChain',
    ...getFixOrSuggest({
      fixOrSuggest: useSuggestionFixer ? 'suggest' : 'fix',
      suggestion: {
        fix,
        messageId: 'optionalChainSuggest',
      },
    }),
  };

  interface FlattenedChain {
    nonNull: boolean;
    optional: boolean;
    precedence: OperatorPrecedence;
    requiresDot: boolean;
    text: string;
  }
  function flattenChainExpression(
    sourceCode: SourceCode,
    node: TSESTree.Node,
  ): FlattenedChain[] {
    switch (node.type) {
      case AST_NODE_TYPES.ChainExpression:
        return flattenChainExpression(sourceCode, node.expression);

      case AST_NODE_TYPES.CallExpression: {
        const argumentsText = (() => {
          const closingParenToken = nullThrows(
            sourceCode.getLastToken(node),
            NullThrowsReasons.MissingToken('closing parenthesis', node.type),
          );
          const openingParenToken = nullThrows(
            sourceCode.getFirstTokenBetween(
              node.typeArguments ?? node.callee,
              closingParenToken,
              isOpeningParenToken,
            ),
            NullThrowsReasons.MissingToken('opening parenthesis', node.type),
          );
          return sourceCode.text.substring(
            openingParenToken.range[0],
            closingParenToken.range[1],
          );
        })();

        const typeArgumentsText = (() => {
          if (node.typeArguments == null) {
            return '';
          }

          return sourceCode.getText(node.typeArguments);
        })();

        return [
          ...flattenChainExpression(sourceCode, node.callee),
          {
            nonNull: false,
            optional: node.optional,
            // no precedence for this
            precedence: OperatorPrecedence.Invalid,
            requiresDot: false,
            text: typeArgumentsText + argumentsText,
          },
        ];
      }

      case AST_NODE_TYPES.MemberExpression: {
        const propertyText = sourceCode.getText(node.property);
        return [
          ...flattenChainExpression(sourceCode, node.object),
          {
            nonNull: node.object.type === AST_NODE_TYPES.TSNonNullExpression,
            optional: node.optional,
            precedence: node.computed
              ? // computed is already wrapped in [] so no need to wrap in () as well
                OperatorPrecedence.Invalid
              : getOperatorPrecedenceForNode(node.property),
            requiresDot: !node.computed,
            text: node.computed ? `[${propertyText}]` : propertyText,
          },
        ];
      }

      case AST_NODE_TYPES.TSNonNullExpression:
        return flattenChainExpression(sourceCode, node.expression);

      default:
        return [
          {
            nonNull: false,
            optional: false,
            precedence: getOperatorPrecedenceForNode(node),
            requiresDot: false,
            text: sourceCode.getText(node),
          },
        ];
    }
  }
}
```
</details>

- **Parameters**:
  - `sourceCode: SourceCode`
  - `parserServices: ParserServicesWithTypeInformation`
  - `node: TSESTree.Node`
  - `operator: '&&' | '||'`
  - `options: PreferOptionalChainOptions`
  - `chain: ValidOperand[]`
- **Return Type**: `ReportDescriptor<PreferOptionalChainMessageIds>`
- **Calls**:
  - `includesType`
  - `flattenChainExpression`
  - `nextOperand.slice`
  - `parts.push`
  - `parts
    .map(part => {
      let str = '';
      if (part.optional) {
        str += '?.';
      } else {
        if (part.nonNull) {
          str += '!';
        }
        if (part.requiresDot) {
          str += '.';
        }
      }
      if (
        part.precedence !== OperatorPrecedence.Invalid &&
        part.precedence < OperatorPrecedence.Member
      ) {
        str += `(${part.text})`;
      } else {
        str += part.text;
      }
      return str;
    })
    .join`
  - `complex_call_12087`
  - `sourceCode.getText`
  - `getReportRange`
  - `fixer.replaceTextRange`
  - `sourceCode.getLocFromIndex`
  - `getFixOrSuggest (from ../../util)`
  - `complex_call_13902`
  - `nullThrows (from ../../util)`
  - `sourceCode.getLastToken`
  - `NullThrowsReasons.MissingToken`
  - `sourceCode.getFirstTokenBetween`
  - `sourceCode.text.substring`
  - `complex_call_14595`
  - `getOperatorPrecedenceForNode (from ../../util)`
- **Internal Comments**:
```
// user has opted-in to the unsafe behavior (x3)
// we know the last operand is an equality check - so the change in types (x3)
// DOES NOT matter and will not change the runtime result or cause a type (x3)
// check error (x3)
// In its most naive form we could just slap `?.` for every single part of the (x2)
// chain. However this would be undesirable because it'd create unnecessary (x2)
// conditions in the user's code where there were none before - and it would (x2)
// cause errors with rules like our `no-unnecessary-condition`. (x2)
// (x6)
// Instead we want to include the minimum number of `?.` required to correctly (x2)
// unify the code into a single chain. Naively you might think that we can (x2)
// just take the final operand add `?.` after the locations from the previous (x2)
// operands - however this won't be correct either because earlier operands (x2)
// can include a necessary `?.` that's not needed or included in a later (x2)
// operand. (x2)
// So instead what we need to do is to start at the first operand and (x2)
// iteratively diff it against the next operand, and add the difference to the (x2)
// first operand. (x2)
// eg (x2)
// `foo && foo.bar && foo.bar.baz?.bam && foo.bar.baz.bam()` (x2)
// 1) `foo` (x2)
// 2) diff(`foo`, `foo.bar`) = `.bar` (x2)
// 3) result = `foo?.bar` (x2)
// 4) diff(`foo.bar`, `foo.bar.baz?.bam`) = `.baz?.bam` (x2)
// 5) result = `foo?.bar?.baz?.bam` (x2)
// 6) diff(`foo.bar.baz?.bam`, `foo.bar.baz.bam()`) = `()` (x2)
// 7) result = `foo?.bar?.baz?.bam?.()` (x2)
// we need to make the first operand of the diff optional so it matches the (x5)
// logic before merging (x5)
// foo.bar && foo.bar.baz (x5)
// diff = .baz (x5)
// result = foo.bar?.baz (x5)
// retain the ending comparison for cases like (x2)
// x && x.a != null (x2)
// x && typeof x.a !== 'undefined' (x2)
// no precedence for this (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
    fixer.replaceTextRange(reportRange, newCode)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceTextRange`
### `flattenChainExpression(sourceCode: SourceCode, node: TSESTree.Node): FlattenedChain[]`

<details><summary>Code</summary>

```ts
function flattenChainExpression(
    sourceCode: SourceCode,
    node: TSESTree.Node,
  ): FlattenedChain[] {
    switch (node.type) {
      case AST_NODE_TYPES.ChainExpression:
        return flattenChainExpression(sourceCode, node.expression);

      case AST_NODE_TYPES.CallExpression: {
        const argumentsText = (() => {
          const closingParenToken = nullThrows(
            sourceCode.getLastToken(node),
            NullThrowsReasons.MissingToken('closing parenthesis', node.type),
          );
          const openingParenToken = nullThrows(
            sourceCode.getFirstTokenBetween(
              node.typeArguments ?? node.callee,
              closingParenToken,
              isOpeningParenToken,
            ),
            NullThrowsReasons.MissingToken('opening parenthesis', node.type),
          );
          return sourceCode.text.substring(
            openingParenToken.range[0],
            closingParenToken.range[1],
          );
        })();

        const typeArgumentsText = (() => {
          if (node.typeArguments == null) {
            return '';
          }

          return sourceCode.getText(node.typeArguments);
        })();

        return [
          ...flattenChainExpression(sourceCode, node.callee),
          {
            nonNull: false,
            optional: node.optional,
            // no precedence for this
            precedence: OperatorPrecedence.Invalid,
            requiresDot: false,
            text: typeArgumentsText + argumentsText,
          },
        ];
      }

      case AST_NODE_TYPES.MemberExpression: {
        const propertyText = sourceCode.getText(node.property);
        return [
          ...flattenChainExpression(sourceCode, node.object),
          {
            nonNull: node.object.type === AST_NODE_TYPES.TSNonNullExpression,
            optional: node.optional,
            precedence: node.computed
              ? // computed is already wrapped in [] so no need to wrap in () as well
                OperatorPrecedence.Invalid
              : getOperatorPrecedenceForNode(node.property),
            requiresDot: !node.computed,
            text: node.computed ? `[${propertyText}]` : propertyText,
          },
        ];
      }

      case AST_NODE_TYPES.TSNonNullExpression:
        return flattenChainExpression(sourceCode, node.expression);

      default:
        return [
          {
            nonNull: false,
            optional: false,
            precedence: getOperatorPrecedenceForNode(node),
            requiresDot: false,
            text: sourceCode.getText(node),
          },
        ];
    }
  }
```
</details>

- **Parameters**:
  - `sourceCode: SourceCode`
  - `node: TSESTree.Node`
- **Return Type**: `FlattenedChain[]`
- **Calls**:
  - `flattenChainExpression`
  - `complex_call_13902`
  - `nullThrows (from ../../util)`
  - `sourceCode.getLastToken`
  - `NullThrowsReasons.MissingToken`
  - `sourceCode.getFirstTokenBetween`
  - `sourceCode.text.substring`
  - `complex_call_14595`
  - `sourceCode.getText`
  - `getOperatorPrecedenceForNode (from ../../util)`
- **Internal Comments**:
```
// no precedence for this (x2)
```

### `analyzeChain(context: RuleContext<
    PreferOptionalChainMessageIds,
    [PreferOptionalChainOptions]
  >, parserServices: ParserServicesWithTypeInformation, options: PreferOptionalChainOptions, node: TSESTree.Node, operator: TSESTree.LogicalExpression['operator'], chain: ValidOperand[]): void`

<details><summary>Code</summary>

```ts
export function analyzeChain(
  context: RuleContext<
    PreferOptionalChainMessageIds,
    [PreferOptionalChainOptions]
  >,
  parserServices: ParserServicesWithTypeInformation,
  options: PreferOptionalChainOptions,
  node: TSESTree.Node,
  operator: TSESTree.LogicalExpression['operator'],
  chain: ValidOperand[],
): void {
  // need at least 2 operands in a chain for it to be a chain
  if (
    chain.length <= 1 ||
    /* istanbul ignore next -- previous checks make this unreachable, but keep it for exhaustiveness check */
    operator === '??'
  ) {
    return;
  }

  const analyzeOperand = (() => {
    switch (operator) {
      case '&&':
        return analyzeAndChainOperand;

      case '||':
        return analyzeOrChainOperand;
    }
  })();

  // Things like x !== null && x !== undefined have two nodes, but they are
  // one logical unit here, so we'll allow them to be grouped.
  let subChain: (readonly ValidOperand[] | ValidOperand)[] = [];
  const maybeReportThenReset = (
    newChainSeed?: readonly [ValidOperand, ...ValidOperand[]],
  ): void => {
    if (subChain.length > 1) {
      const subChainFlat = subChain.flat();
      checkNullishAndReport(
        context,
        parserServices,
        options,
        subChainFlat.slice(0, -1).map(({ node }) => node),
        getReportDescriptor(
          context.sourceCode,
          parserServices,
          node,
          operator,
          options,
          subChainFlat,
        ),
      );
    }

    // we've reached the end of a chain of logical expressions
    // i.e. the current operand doesn't belong to the previous chain.
    //
    // we don't want to throw away the current operand otherwise we will skip it
    // and that can cause us to miss chains. So instead we seed the new chain
    // with the current operand
    //
    // eg this means we can catch cases like:
    //     unrelated != null && foo != null && foo.bar != null;
    //     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ first "chain"
    //                          ^^^^^^^^^^^ newChainSeed
    //                          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ second chain
    subChain = newChainSeed ? [newChainSeed] : [];
  };

  for (let i = 0; i < chain.length; i += 1) {
    const lastOperand = subChain.flat().at(-1);
    const operand = chain[i];

    const validatedOperands = analyzeOperand(parserServices, operand, i, chain);
    if (!validatedOperands) {
      // TODO - #7170
      // check if the name is a superset/equal - if it is, then it likely
      // intended to be part of the chain and something we should include in the
      // report, eg
      //     foo == null || foo.bar;
      //     ^^^^^^^^^^^ valid OR chain
      //                    ^^^^^^^ invalid OR chain logical, but still part of
      //                            the chain for combination purposes

      maybeReportThenReset();
      continue;
    }
    // in case multiple operands were consumed - make sure to correctly increment the index
    i += validatedOperands.length - 1;

    const currentOperand = validatedOperands[0];
    if (lastOperand) {
      const comparisonResult = compareNodes(
        lastOperand.comparedName,
        // purposely inspect and push the last operand because the prior operands don't matter
        // this also means we won't false-positive in cases like
        // foo !== null && foo !== undefined
        validatedOperands[validatedOperands.length - 1].comparedName,
      );
      if (comparisonResult === NodeComparisonResult.Subset) {
        // the operands are comparable, so we can continue searching
        subChain.push(currentOperand);
      } else if (comparisonResult === NodeComparisonResult.Invalid) {
        maybeReportThenReset(validatedOperands);
      } else {
        // purposely don't push this case because the node is a no-op and if
        // we consider it then we might report on things like
        // foo && foo
      }
    } else {
      subChain.push(currentOperand);
    }
  }

  // check the leftovers
  maybeReportThenReset();
}
```
</details>

- **Parameters**:
  - `context: RuleContext<
    PreferOptionalChainMessageIds,
    [PreferOptionalChainOptions]
  >`
  - `parserServices: ParserServicesWithTypeInformation`
  - `options: PreferOptionalChainOptions`
  - `node: TSESTree.Node`
  - `operator: TSESTree.LogicalExpression['operator']`
  - `chain: ValidOperand[]`
- **Return Type**: `void`
- **Calls**:
  - `complex_call_16801`
  - `subChain.flat`
  - `checkNullishAndReport (from ./checkNullishAndReport)`
  - `subChainFlat.slice(0, -1).map`
  - `getReportDescriptor`
  - `subChain.flat().at`
  - `analyzeOperand`
  - `maybeReportThenReset`
  - `compareNodes (from ./compareNodes)`
  - `subChain.push`
- **Internal Comments**:
```
// need at least 2 operands in a chain for it to be a chain
/* istanbul ignore next -- previous checks make this unreachable, but keep it for exhaustiveness check */ (x2)
// Things like x !== null && x !== undefined have two nodes, but they are (x2)
// one logical unit here, so we'll allow them to be grouped. (x2)
// we've reached the end of a chain of logical expressions (x3)
// i.e. the current operand doesn't belong to the previous chain. (x3)
// (x6)
// we don't want to throw away the current operand otherwise we will skip it (x3)
// and that can cause us to miss chains. So instead we seed the new chain (x3)
// with the current operand (x3)
// eg this means we can catch cases like: (x3)
//     unrelated != null && foo != null && foo.bar != null; (x3)
//     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ first "chain" (x3)
//                          ^^^^^^^^^^^ newChainSeed (x3)
//                          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ second chain (x3)
// TODO - #7170 (x3)
// check if the name is a superset/equal - if it is, then it likely (x3)
// intended to be part of the chain and something we should include in the (x3)
// report, eg (x3)
//     foo == null || foo.bar; (x3)
//     ^^^^^^^^^^^ valid OR chain (x3)
//                    ^^^^^^^ invalid OR chain logical, but still part of (x3)
//                            the chain for combination purposes (x3)
// in case multiple operands were consumed - make sure to correctly increment the index (x3)
// purposely inspect and push the last operand because the prior operands don't matter (x3)
// this also means we won't false-positive in cases like (x3)
// foo !== null && foo !== undefined (x3)
// the operands are comparable, so we can continue searching (x4)
// check the leftovers (x3)
```

### `maybeReportThenReset(newChainSeed: readonly [ValidOperand, ...ValidOperand[]]): void`

<details><summary>Code</summary>

```ts
(
    newChainSeed?: readonly [ValidOperand, ...ValidOperand[]],
  ): void => {
    if (subChain.length > 1) {
      const subChainFlat = subChain.flat();
      checkNullishAndReport(
        context,
        parserServices,
        options,
        subChainFlat.slice(0, -1).map(({ node }) => node),
        getReportDescriptor(
          context.sourceCode,
          parserServices,
          node,
          operator,
          options,
          subChainFlat,
        ),
      );
    }

    // we've reached the end of a chain of logical expressions
    // i.e. the current operand doesn't belong to the previous chain.
    //
    // we don't want to throw away the current operand otherwise we will skip it
    // and that can cause us to miss chains. So instead we seed the new chain
    // with the current operand
    //
    // eg this means we can catch cases like:
    //     unrelated != null && foo != null && foo.bar != null;
    //     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ first "chain"
    //                          ^^^^^^^^^^^ newChainSeed
    //                          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ second chain
    subChain = newChainSeed ? [newChainSeed] : [];
  }
```
</details>

- **Parameters**:
  - `newChainSeed: readonly [ValidOperand, ...ValidOperand[]]`
- **Return Type**: `void`
- **Calls**:
  - `subChain.flat`
  - `checkNullishAndReport (from ./checkNullishAndReport)`
  - `subChainFlat.slice(0, -1).map`
  - `getReportDescriptor`
- **Internal Comments**:
```
// we've reached the end of a chain of logical expressions (x3)
// i.e. the current operand doesn't belong to the previous chain. (x3)
// (x6)
// we don't want to throw away the current operand otherwise we will skip it (x3)
// and that can cause us to miss chains. So instead we seed the new chain (x3)
// with the current operand (x3)
// eg this means we can catch cases like: (x3)
//     unrelated != null && foo != null && foo.bar != null; (x3)
//     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ first "chain" (x3)
//                          ^^^^^^^^^^^ newChainSeed (x3)
//                          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ second chain (x3)
```


---

## Interfaces

### `FlattenedChain`

<details><summary>Interface Code</summary>

```ts
interface FlattenedChain {
    nonNull: boolean;
    optional: boolean;
    precedence: OperatorPrecedence;
    requiresDot: boolean;
    text: string;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `nonNull` | `boolean` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `precedence` | `OperatorPrecedence` | ✗ |  |
| `requiresDot` | `boolean` | ✗ |  |
| `text` | `string` | ✗ |  |


---

## Type Aliases

### `OperandAnalyzer`

```ts
type OperandAnalyzer = (
  parserServices: ParserServicesWithTypeInformation,
  operand: ValidOperand,
  index: number,
  chain: readonly ValidOperand[],
) => readonly [ValidOperand, ValidOperand] | readonly [ValidOperand] | null;
```


---