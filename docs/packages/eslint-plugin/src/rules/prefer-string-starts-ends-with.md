[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-string-starts-ends-with.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 16 |
| 📦 Imports | 14 |
| 📊 Variables & Constants | 28 |
| 📑 Type Aliases | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-string-starts-ends-with.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `RegExpParser` | `@eslint-community/regexpp` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `getPropertyName` | `../util` |
| `getStaticValue` | `../util` |
| `getTypeName` | `../util` |
| `isNotClosingParenToken` | `../util` |
| `isStaticMemberAccessOfValue` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |
| `skipChainExpression` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `EQ_OPERATORS` | `RegExp` | const | `/^[=!]=/` | ✗ |
| `regexpp` | `any` | const | `new RegExpParser()` | ✗ |
| `token1` | `any` | const | `tokens1[i]` | ✗ |
| `token2` | `any` | const | `tokens2[i]` | ✗ |
| `chars` | `any` | const | `ast.alternatives[0].elements` | ✗ |
| `first` | `any` | const | `chars[0]` | ✗ |
| `leftNode` | `any` | const | `node.type === AST_NODE_TYPES.CallExpression ? node.callee : node` | ✗ |
| `indexNode` | `TSESTree.Node | null` | let/var | `null` | ✗ |
| `isStartsWith` | `boolean` | const | `!isEndsWith && isNumber(indexNode, 0)` | ✗ |
| `eqNode` | `TSESTree.BinaryExpression` | const | `parentNode` | ✗ |
| `callNode` | `TSESTree.CallExpression` | const | `getParent(node) as TSESTree.CallExpression` | ✗ |
| `callNode` | `TSESTree.CallExpression` | const | `getParent(node) as TSESTree.CallExpression` | ✗ |
| `callNode` | `TSESTree.CallExpression` | const | `getParent(node) as TSESTree.CallExpression` | ✗ |
| `parentNode` | `TSESTree.BinaryExpression` | const | `getParent(callNode) as TSESTree.BinaryExpression` | ✗ |
| `parsed` | `{ isEndsWith: boolean; isStartsWith: boolean; text: string; }` | const | `callNode.arguments.length === 1
            ? parseRegExp(callNode.arguments[0])
            : null` | ✗ |
| `callNode` | `TSESTree.CallExpression` | const | `getParent(node) as TSESTree.CallExpression` | ✗ |
| `isEndsWith` | `boolean` | let/var | `false` | ✗ |
| `isStartsWith` | `boolean` | let/var | `false` | ✗ |
| `eqNode` | `TSESTree.BinaryExpression` | const | `parentNode` | ✗ |
| `negativeIndexSupported` | `boolean` | const | `(node.property as TSESTree.Identifier).name === 'slice'` | ✗ |
| `posNode` | `any` | const | `callNode.arguments[0]` | ✗ |
| `posNodeIsAbsolutelyValid` | `boolean` | const | `(posNode.type === AST_NODE_TYPES.BinaryExpression &&
                  posNode.operator === '-' &&
                  isLengthExpression(posNode.left, node.object) &&
                  isLengthExpression(posNode.right, eqNode.right)) ||
                (negativeIndexSupported &&
                  posNode.type === AST_NODE_TYPES.UnaryExpression &&
                  posNode.operator === '-' &&
                  isLengthExpression(posNode.argument, eqNode.right))` | ✗ |
| `callNode` | `TSESTree.CallExpression` | const | `getParent(node) as TSESTree.CallExpression` | ✗ |
| `parsed` | `{ isEndsWith: boolean; isStartsWith: boolean; text: string; }` | const | `callNode.arguments.length === 1 ? parseRegExp(node.object) : null` | ✗ |
| `messageId` | `"preferEndsWith" | "preferStartsWith"` | const | `isStartsWith ? 'preferStartsWith' : 'preferEndsWith'` | ✗ |
| `methodName` | `"startsWith" | "endsWith"` | const | `isStartsWith ? 'startsWith' : 'endsWith'` | ✗ |
| `argNode` | `any` | let/var | `callNode.arguments[0]` | ✗ |
| `needsParen` | `boolean` | let/var | `argNode.type !== AST_NODE_TYPES.Literal &&
              argNode.type !== AST_NODE_TYPES.TemplateLiteral &&
              argNode.type !== AST_NODE_TYPES.Identifier &&
              argNode.type !== AST_NODE_TYPES.MemberExpression &&
              argNode.type !== AST_NODE_TYPES.CallExpression` | ✗ |


---

## Functions

### `isStringType(node: TSESTree.Expression): boolean`

<details><summary>Code</summary>

```ts
function isStringType(node: TSESTree.Expression): boolean {
      const objectType = services.getTypeAtLocation(node);
      return getTypeName(checker, objectType) === 'string';
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if a given node is a string.
     * @param node The node to check.
     */
```

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `boolean`
- **Calls**:
  - `services.getTypeAtLocation`
  - `getTypeName (from ../util)`
### `isNull(node: TSESTree.Node): node is TSESTree.Literal`

<details><summary>Code</summary>

```ts
function isNull(node: TSESTree.Node): node is TSESTree.Literal {
      const evaluated = getStaticValue(node, globalScope);
      return evaluated != null && evaluated.value == null;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if a given node is a `Literal` node that is null.
     * @param node The node to check.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.Literal`
- **Calls**:
  - `getStaticValue (from ../util)`
### `isNumber(node: TSESTree.Node, value: number): node is TSESTree.Literal`

<details><summary>Code</summary>

```ts
function isNumber(
      node: TSESTree.Node,
      value: number,
    ): node is TSESTree.Literal {
      const evaluated = getStaticValue(node, globalScope);
      return evaluated != null && evaluated.value === value;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if a given node is a `Literal` node that is a given value.
     * @param node The node to check.
     * @param value The expected value of the `Literal` node.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `value: number`
- **Return Type**: `node is TSESTree.Literal`
- **Calls**:
  - `getStaticValue (from ../util)`
### `isCharacter(node: TSESTree.Node): node is TSESTree.Literal`

<details><summary>Code</summary>

```ts
function isCharacter(node: TSESTree.Node): node is TSESTree.Literal {
      const evaluated = getStaticValue(node, globalScope);
      return (
        evaluated != null &&
        typeof evaluated.value === 'string' &&
        // checks if the string is a character long
        evaluated.value[0] === evaluated.value
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if a given node is a `Literal` node that is a character.
     * @param node The node to check.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.Literal`
- **Calls**:
  - `getStaticValue (from ../util)`
- **Internal Comments**:
```
// checks if the string is a character long (x4)
```

### `isEqualityComparison(node: TSESTree.Node): node is TSESTree.BinaryExpression`

<details><summary>Code</summary>

```ts
function isEqualityComparison(
      node: TSESTree.Node,
    ): node is TSESTree.BinaryExpression {
      return (
        node.type === AST_NODE_TYPES.BinaryExpression &&
        EQ_OPERATORS.test(node.operator)
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if a given node is `==`, `===`, `!=`, or `!==`.
     * @param node The node to check.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.BinaryExpression`
- **Calls**:
  - `EQ_OPERATORS.test`
### `isSameTokens(node1: TSESTree.Node, node2: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isSameTokens(node1: TSESTree.Node, node2: TSESTree.Node): boolean {
      const tokens1 = context.sourceCode.getTokens(node1);
      const tokens2 = context.sourceCode.getTokens(node2);

      if (tokens1.length !== tokens2.length) {
        return false;
      }

      for (let i = 0; i < tokens1.length; ++i) {
        const token1 = tokens1[i];
        const token2 = tokens2[i];

        if (token1.type !== token2.type || token1.value !== token2.value) {
          return false;
        }
      }

      return true;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if two given nodes are the same meaning.
     * @param node1 A node to compare.
     * @param node2 Another node to compare.
     */
```

- **Parameters**:
  - `node1: TSESTree.Node`
  - `node2: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode.getTokens`
### `isLengthExpression(node: TSESTree.Node, expectedObjectNode: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isLengthExpression(
      node: TSESTree.Node,
      expectedObjectNode: TSESTree.Node,
    ): boolean {
      if (node.type === AST_NODE_TYPES.MemberExpression) {
        return (
          getPropertyName(node, globalScope) === 'length' &&
          isSameTokens(node.object, expectedObjectNode)
        );
      }

      const evaluatedLength = getStaticValue(node, globalScope);
      const evaluatedString = getStaticValue(expectedObjectNode, globalScope);
      return (
        evaluatedLength != null &&
        evaluatedString != null &&
        typeof evaluatedLength.value === 'number' &&
        typeof evaluatedString.value === 'string' &&
        evaluatedLength.value === evaluatedString.value.length
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if a given node is the expression of the length of a string.
     *
     * - If `length` property access of `expectedObjectNode`, it's `true`.
     *   E.g., `foo` → `foo.length` / `"foo"` → `"foo".length`
     * - If `expectedObjectNode` is a string literal, `node` can be a number.
     *   E.g., `"foo"` → `3`
     *
     * @param node The node to check.
     * @param expectedObjectNode The node which is expected as the receiver of `length` property.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `expectedObjectNode: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `getPropertyName (from ../util)`
  - `isSameTokens`
  - `getStaticValue (from ../util)`
### `isLengthAheadOfEnd(node: TSESTree.Node, substring: TSESTree.Node, parentString: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isLengthAheadOfEnd(
      node: TSESTree.Node,
      substring: TSESTree.Node,
      parentString: TSESTree.Node,
    ): boolean {
      return (
        (node.type === AST_NODE_TYPES.UnaryExpression &&
          node.operator === '-' &&
          isLengthExpression(node.argument, substring)) ||
        (node.type === AST_NODE_TYPES.BinaryExpression &&
          node.operator === '-' &&
          isLengthExpression(node.left, parentString) &&
          isLengthExpression(node.right, substring))
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Returns true if `node` is `-substring.length` or
     * `parentString.length - substring.length`
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `substring: TSESTree.Node`
  - `parentString: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isLengthExpression`
### `isLastIndexExpression(node: TSESTree.Node, expectedObjectNode: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isLastIndexExpression(
      node: TSESTree.Node,
      expectedObjectNode: TSESTree.Node,
    ): boolean {
      return (
        node.type === AST_NODE_TYPES.BinaryExpression &&
        node.operator === '-' &&
        isLengthExpression(node.left, expectedObjectNode) &&
        isNumber(node.right, 1)
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if a given node is the expression of the last index.
     *
     * E.g. `foo.length - 1`
     *
     * @param node The node to check.
     * @param expectedObjectNode The node which is expected as the receiver of `length` property.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `expectedObjectNode: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isLengthExpression`
  - `isNumber`
### `getPropertyRange(node: TSESTree.MemberExpression): [number, number]`

<details><summary>Code</summary>

```ts
function getPropertyRange(
      node: TSESTree.MemberExpression,
    ): [number, number] {
      const dotOrOpenBracket = nullThrows(
        context.sourceCode.getTokenAfter(node.object, isNotClosingParenToken),
        NullThrowsReasons.MissingToken('closing parenthesis', 'member'),
      );
      return [dotOrOpenBracket.range[0], node.range[1]];
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Get the range of the property of a given `MemberExpression` node.
     *
     * - `obj[foo]` → the range of `[foo]`
     * - `obf.foo` → the range of `.foo`
     * - `(obj).foo` → the range of `.foo`
     *
     * @param node The member expression node to get.
     */
```

- **Parameters**:
  - `node: TSESTree.MemberExpression`
- **Return Type**: `[number, number]`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenAfter`
  - `NullThrowsReasons.MissingToken`
### `parseRegExpText(pattern: string, unicode: boolean): string | null`

<details><summary>Code</summary>

```ts
function parseRegExpText(pattern: string, unicode: boolean): string | null {
      // Parse it.
      const ast = regexpp.parsePattern(pattern, undefined, undefined, {
        unicode,
      });
      if (ast.alternatives.length !== 1) {
        return null;
      }

      // Drop `^`/`$` assertion.
      const chars = ast.alternatives[0].elements;
      const first = chars[0];
      if (first.type === 'Assertion' && first.kind === 'start') {
        chars.shift();
      } else {
        chars.pop();
      }

      // Check if it can determine a unique string.
      if (!chars.every(c => c.type === 'Character')) {
        return null;
      }

      // To string.
      return String.fromCodePoint(...chars.map(c => c.value));
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Parse a given `RegExp` pattern to that string if it's a static string.
     * @param pattern The RegExp pattern text to parse.
     * @param unicode Whether the RegExp is unicode.
     */
```

- **Parameters**:
  - `pattern: string`
  - `unicode: boolean`
- **Return Type**: `string | null`
- **Calls**:
  - `regexpp.parsePattern`
  - `chars.shift`
  - `chars.pop`
  - `chars.every`
  - `String.fromCodePoint`
  - `chars.map`
- **Internal Comments**:
```
// Parse it. (x2)
// Drop `^`/`$` assertion. (x2)
// Check if it can determine a unique string.
// To string.
```

### `parseRegExp(node: TSESTree.Node): { isEndsWith: boolean; isStartsWith: boolean; text: string } | null`

<details><summary>Code</summary>

```ts
function parseRegExp(
      node: TSESTree.Node,
    ): { isEndsWith: boolean; isStartsWith: boolean; text: string } | null {
      const evaluated = getStaticValue(node, globalScope);
      if (evaluated == null || !(evaluated.value instanceof RegExp)) {
        return null;
      }

      const { flags, source } = evaluated.value;
      const isStartsWith = source.startsWith('^');
      const isEndsWith = source.endsWith('$');
      if (
        isStartsWith === isEndsWith ||
        flags.includes('i') ||
        flags.includes('m')
      ) {
        return null;
      }

      const text = parseRegExpText(source, flags.includes('u'));
      if (text == null) {
        return null;
      }

      return { isEndsWith, isStartsWith, text };
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Parse a given node if it's a `RegExp` instance.
     * @param node The node to parse.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `{ isEndsWith: boolean; isStartsWith: boolean; text: string } | null`
- **Calls**:
  - `getStaticValue (from ../util)`
  - `source.startsWith`
  - `source.endsWith`
  - `flags.includes`
  - `parseRegExpText`
### `getLeftNode(init: TSESTree.Expression | TSESTree.PrivateIdentifier): TSESTree.MemberExpression`

<details><summary>Code</summary>

```ts
function getLeftNode(
      init: TSESTree.Expression | TSESTree.PrivateIdentifier,
    ): TSESTree.MemberExpression {
      const node = skipChainExpression(init);
      const leftNode =
        node.type === AST_NODE_TYPES.CallExpression ? node.callee : node;

      if (leftNode.type !== AST_NODE_TYPES.MemberExpression) {
        throw new Error(`Expected a MemberExpression, got ${leftNode.type}`);
      }

      return leftNode;
    }
```
</details>

- **Parameters**:
  - `init: TSESTree.Expression | TSESTree.PrivateIdentifier`
- **Return Type**: `TSESTree.MemberExpression`
- **Calls**:
  - `skipChainExpression (from ../util)`
### `fixWithRightOperand(fixer: TSESLint.RuleFixer, node: TSESTree.BinaryExpression, kind: 'end' | 'start', isNegative: boolean, isOptional: boolean): IterableIterator<TSESLint.RuleFix>`

<details><summary>Code</summary>

```ts
function* fixWithRightOperand(
      fixer: TSESLint.RuleFixer,
      node: TSESTree.BinaryExpression,
      kind: 'end' | 'start',
      isNegative: boolean,
      isOptional: boolean,
    ): IterableIterator<TSESLint.RuleFix> {
      // left is CallExpression or MemberExpression.
      const leftNode = getLeftNode(node.left);
      const propertyRange = getPropertyRange(leftNode);

      if (isNegative) {
        yield fixer.insertTextBefore(node, '!');
      }
      yield fixer.replaceTextRange(
        [propertyRange[0], node.right.range[0]],
        `${isOptional ? '?.' : '.'}${kind}sWith(`,
      );
      yield fixer.replaceTextRange([node.right.range[1], node.range[1]], ')');
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Fix code with using the right operand as the search string.
     * For example: `foo.slice(0, 3) === 'bar'` → `foo.startsWith('bar')`
     * @param fixer The rule fixer.
     * @param node The node which was reported.
     * @param kind The kind of the report.
     * @param isNegative The flag to fix to negative condition.
     */
```

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `node: TSESTree.BinaryExpression`
  - `kind: 'end' | 'start'`
  - `isNegative: boolean`
  - `isOptional: boolean`
- **Return Type**: `IterableIterator<TSESLint.RuleFix>`
- **Calls**:
  - `getLeftNode`
  - `getPropertyRange`
  - `fixer.insertTextBefore`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// left is CallExpression or MemberExpression. (x2)
```

### `fixWithArgument(fixer: TSESLint.RuleFixer, node: TSESTree.BinaryExpression, callNode: TSESTree.CallExpression, calleeNode: TSESTree.MemberExpression, kind: 'end' | 'start', negative: boolean, isOptional: boolean): IterableIterator<TSESLint.RuleFix>`

<details><summary>Code</summary>

```ts
function* fixWithArgument(
      fixer: TSESLint.RuleFixer,
      node: TSESTree.BinaryExpression,
      callNode: TSESTree.CallExpression,
      calleeNode: TSESTree.MemberExpression,
      kind: 'end' | 'start',
      negative: boolean,
      isOptional: boolean,
    ): IterableIterator<TSESLint.RuleFix> {
      if (negative) {
        yield fixer.insertTextBefore(node, '!');
      }
      yield fixer.replaceTextRange(
        getPropertyRange(calleeNode),
        `${isOptional ? '?.' : '.'}${kind}sWith`,
      );
      yield fixer.removeRange([callNode.range[1], node.range[1]]);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Fix code with using the first argument as the search string.
     * For example: `foo.indexOf('bar') === 0` → `foo.startsWith('bar')`
     * @param fixer The rule fixer.
     * @param node The node which was reported.
     * @param kind The kind of the report.
     * @param negative The flag to fix to negative condition.
     */
```

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `node: TSESTree.BinaryExpression`
  - `callNode: TSESTree.CallExpression`
  - `calleeNode: TSESTree.MemberExpression`
  - `kind: 'end' | 'start'`
  - `negative: boolean`
  - `isOptional: boolean`
- **Return Type**: `IterableIterator<TSESLint.RuleFix>`
- **Calls**:
  - `fixer.insertTextBefore`
  - `fixer.replaceTextRange`
  - `getPropertyRange`
  - `fixer.removeRange`
### `getParent(node: TSESTree.Node): TSESTree.Node`

<details><summary>Code</summary>

```ts
function getParent(node: TSESTree.Node): TSESTree.Node {
      return nullThrows(
        node.parent?.type === AST_NODE_TYPES.ChainExpression
          ? node.parent.parent
          : node.parent,
        NullThrowsReasons.MissingParent,
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `TSESTree.Node`
- **Calls**:
  - `nullThrows (from ../util)`

---

## Type Aliases

### `AllowedSingleElementEquality`

```ts
type AllowedSingleElementEquality = 'always' | 'never';
```

### `Options`

```ts
type Options = [
  {
    allowSingleElementEquality?: AllowedSingleElementEquality;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'preferEndsWith' | 'preferStartsWith';
```


---