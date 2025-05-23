[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `node-utils.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 48
- **Classes**: 1
- **Imports**: 7
- **Interfaces**: 1
- **Type Aliases**: 5

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/node-utils.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `./ts-estree` |
| `TSNode` | `./ts-estree` |
| `getModifiers` | `./getModifiers` |
| `xhtmlEntities` | `./jsx/xhtml-entities` |
| `AST_NODE_TYPES` | `./ts-estree` |
| `AST_TOKEN_TYPES` | `./ts-estree` |
| `typescriptVersionIsAtLeast` | `./version-check` |


---

## Functions

### `isAssignmentOperator(operator: ts.BinaryOperatorToken): operator is ts.Token<AssignmentOperatorKind>`

<details><summary>Code</summary>

```ts
function isAssignmentOperator(
  operator: ts.BinaryOperatorToken,
): operator is ts.Token<AssignmentOperatorKind> {
  return (ASSIGNMENT_OPERATORS as ReadonlySet<ts.SyntaxKind>).has(
    operator.kind,
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if the given ts.Token is the assignment operator
 */
```

- **Parameters**:
  - `operator: ts.BinaryOperatorToken`
- **Return Type**: `operator is ts.Token<AssignmentOperatorKind>`
- **Calls**:
  - `(ASSIGNMENT_OPERATORS as ReadonlySet<ts.SyntaxKind>).has`
### `isLogicalOperator(operator: ts.BinaryOperatorToken): operator is ts.Token<LogicalOperatorKind>`

<details><summary>Code</summary>

```ts
export function isLogicalOperator(
  operator: ts.BinaryOperatorToken,
): operator is ts.Token<LogicalOperatorKind> {
  return (LOGICAL_OPERATORS as ReadonlySet<ts.SyntaxKind>).has(operator.kind);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if the given ts.Token is a logical operator
 */
```

- **Parameters**:
  - `operator: ts.BinaryOperatorToken`
- **Return Type**: `operator is ts.Token<LogicalOperatorKind>`
- **Calls**:
  - `(LOGICAL_OPERATORS as ReadonlySet<ts.SyntaxKind>).has`
### `isESTreeBinaryOperator(operator: ts.BinaryOperatorToken): operator is ts.Token<BinaryOperatorKind>`

<details><summary>Code</summary>

```ts
export function isESTreeBinaryOperator(
  operator: ts.BinaryOperatorToken,
): operator is ts.Token<BinaryOperatorKind> {
  return (BINARY_OPERATORS as ReadonlySet<ts.SyntaxKind>).has(operator.kind);
}
```
</details>

- **Parameters**:
  - `operator: ts.BinaryOperatorToken`
- **Return Type**: `operator is ts.Token<BinaryOperatorKind>`
- **Calls**:
  - `(BINARY_OPERATORS as ReadonlySet<ts.SyntaxKind>).has`
### `getTextForTokenKind(kind: T): TokenForTokenKind<T>`

<details><summary>Code</summary>

```ts
export function getTextForTokenKind<T extends ts.SyntaxKind>(
  kind: T,
): TokenForTokenKind<T> {
  return ts.tokenToString(kind) as T extends keyof TokenToText
    ? TokenToText[T]
    : string | undefined;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns the string form of the given TSToken SyntaxKind
 */
```

- **Parameters**:
  - `kind: T`
- **Return Type**: `TokenForTokenKind<T>`
- **Calls**:
  - `ts.tokenToString`
### `isESTreeClassMember(node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
export function isESTreeClassMember(node: ts.Node): boolean {
  return node.kind !== SyntaxKind.SemicolonClassElement;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if the given ts.Node is a valid ESTree class member
 */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `boolean`
### `hasModifier(modifierKind: ts.KeywordSyntaxKind, node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
export function hasModifier(
  modifierKind: ts.KeywordSyntaxKind,
  node: ts.Node,
): boolean {
  const modifiers = getModifiers(node);
  return modifiers?.some(modifier => modifier.kind === modifierKind) === true;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a ts.Node has a modifier
 */
```

- **Parameters**:
  - `modifierKind: ts.KeywordSyntaxKind`
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `getModifiers (from ./getModifiers)`
  - `modifiers?.some`
### `getLastModifier(node: ts.Node): ts.Modifier | null`

<details><summary>Code</summary>

```ts
export function getLastModifier(node: ts.Node): ts.Modifier | null {
  const modifiers = getModifiers(node);
  if (modifiers == null) {
    return null;
  }
  return modifiers[modifiers.length - 1] ?? null;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Get last last modifier in ast
 * @returns returns last modifier if present or null
 */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `ts.Modifier | null`
- **Calls**:
  - `getModifiers (from ./getModifiers)`
### `isComma(token: ts.Node): token is ts.Token<ts.SyntaxKind.CommaToken>`

<details><summary>Code</summary>

```ts
export function isComma(
  token: ts.Node,
): token is ts.Token<ts.SyntaxKind.CommaToken> {
  return token.kind === SyntaxKind.CommaToken;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if the given ts.Token is a comma
 */
```

- **Parameters**:
  - `token: ts.Node`
- **Return Type**: `token is ts.Token<ts.SyntaxKind.CommaToken>`
### `isComment(node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
export function isComment(node: ts.Node): boolean {
  return (
    node.kind === SyntaxKind.SingleLineCommentTrivia ||
    node.kind === SyntaxKind.MultiLineCommentTrivia
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if the given ts.Node is a comment
 */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `boolean`
### `isJSDocComment(node: ts.Node): node is ts.JSDoc`

<details><summary>Code</summary>

```ts
function isJSDocComment(node: ts.Node): node is ts.JSDoc {
  // eslint-disable-next-line @typescript-eslint/no-deprecated -- SyntaxKind.JSDoc was only added in TS4.7 so we can't use it yet
  return node.kind === SyntaxKind.JSDocComment;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if the given ts.Node is a JSDoc comment
 */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `node is ts.JSDoc`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-deprecated -- SyntaxKind.JSDoc was only added in TS4.7 so we can't use it yet
```

### `getBinaryExpressionType(operator: ts.BinaryOperatorToken): | {
      operator: TokenForTokenKind<AssignmentOperatorKind>;
      type: AST_NODE_TYPES.AssignmentExpression;
    }
  | {
      operator: TokenForTokenKind<BinaryOperatorKind>;
      type: AST_NODE_TYPES.BinaryExpression;
    }
  | {
      operator: TokenForTokenKind<LogicalOperatorKind>;
      type: AST_NODE_TYPES.LogicalExpression;
    }`

<details><summary>Code</summary>

```ts
export function getBinaryExpressionType(operator: ts.BinaryOperatorToken):
  | {
      operator: TokenForTokenKind<AssignmentOperatorKind>;
      type: AST_NODE_TYPES.AssignmentExpression;
    }
  | {
      operator: TokenForTokenKind<BinaryOperatorKind>;
      type: AST_NODE_TYPES.BinaryExpression;
    }
  | {
      operator: TokenForTokenKind<LogicalOperatorKind>;
      type: AST_NODE_TYPES.LogicalExpression;
    } {
  if (isAssignmentOperator(operator)) {
    return {
      type: AST_NODE_TYPES.AssignmentExpression,
      operator: getTextForTokenKind(operator.kind),
    };
  }

  if (isLogicalOperator(operator)) {
    return {
      type: AST_NODE_TYPES.LogicalExpression,
      operator: getTextForTokenKind(operator.kind),
    };
  }

  if (isESTreeBinaryOperator(operator)) {
    return {
      type: AST_NODE_TYPES.BinaryExpression,
      operator: getTextForTokenKind(operator.kind),
    };
  }

  throw new Error(
    `Unexpected binary operator ${ts.tokenToString(operator.kind)}`,
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns the binary expression type of the given ts.Token
 */
```

- **Parameters**:
  - `operator: ts.BinaryOperatorToken`
- **Return Type**: `| {
      operator: TokenForTokenKind<AssignmentOperatorKind>;
      type: AST_NODE_TYPES.AssignmentExpression;
    }
  | {
      operator: TokenForTokenKind<BinaryOperatorKind>;
      type: AST_NODE_TYPES.BinaryExpression;
    }
  | {
      operator: TokenForTokenKind<LogicalOperatorKind>;
      type: AST_NODE_TYPES.LogicalExpression;
    }`
- **Calls**:
  - `isAssignmentOperator`
  - `getTextForTokenKind`
  - `isLogicalOperator`
  - `isESTreeBinaryOperator`
  - `ts.tokenToString`
### `getLineAndCharacterFor(pos: number, ast: ts.SourceFile): TSESTree.Position`

<details><summary>Code</summary>

```ts
export function getLineAndCharacterFor(
  pos: number,
  ast: ts.SourceFile,
): TSESTree.Position {
  const loc = ast.getLineAndCharacterOfPosition(pos);
  return {
    column: loc.character,
    line: loc.line + 1,
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns line and column data for the given positions
 */
```

- **Parameters**:
  - `pos: number`
  - `ast: ts.SourceFile`
- **Return Type**: `TSESTree.Position`
- **Calls**:
  - `ast.getLineAndCharacterOfPosition`
### `getLocFor(range: TSESTree.Range, ast: ts.SourceFile): TSESTree.SourceLocation`

<details><summary>Code</summary>

```ts
export function getLocFor(
  range: TSESTree.Range,
  ast: ts.SourceFile,
): TSESTree.SourceLocation {
  const [start, end] = range.map(pos => getLineAndCharacterFor(pos, ast));
  return { end, start };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns line and column data for the given start and end positions,
 * for the given AST
 */
```

- **Parameters**:
  - `range: TSESTree.Range`
  - `ast: ts.SourceFile`
- **Return Type**: `TSESTree.SourceLocation`
- **Calls**:
  - `range.map`
  - `getLineAndCharacterFor`
### `canContainDirective(node: | ts.Block
    | ts.ClassStaticBlockDeclaration
    | ts.ModuleBlock
    | ts.SourceFile): boolean`

<details><summary>Code</summary>

```ts
export function canContainDirective(
  node:
    | ts.Block
    | ts.ClassStaticBlockDeclaration
    | ts.ModuleBlock
    | ts.SourceFile,
): boolean {
  if (node.kind === ts.SyntaxKind.Block) {
    switch (node.parent.kind) {
      case ts.SyntaxKind.Constructor:
      case ts.SyntaxKind.GetAccessor:
      case ts.SyntaxKind.SetAccessor:
      case ts.SyntaxKind.ArrowFunction:
      case ts.SyntaxKind.FunctionExpression:
      case ts.SyntaxKind.FunctionDeclaration:
      case ts.SyntaxKind.MethodDeclaration:
        return true;
      default:
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
 * Check whatever node can contain directive
 */
```

- **Parameters**:
  - `node: | ts.Block
    | ts.ClassStaticBlockDeclaration
    | ts.ModuleBlock
    | ts.SourceFile`
- **Return Type**: `boolean`
### `getRange(node: Pick<ts.Node, 'getEnd' | 'getStart'>, ast: ts.SourceFile): [number, number]`

<details><summary>Code</summary>

```ts
export function getRange(
  node: Pick<ts.Node, 'getEnd' | 'getStart'>,
  ast: ts.SourceFile,
): [number, number] {
  return [node.getStart(ast), node.getEnd()];
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns range for the given ts.Node
 */
```

- **Parameters**:
  - `node: Pick<ts.Node, 'getEnd' | 'getStart'>`
  - `ast: ts.SourceFile`
- **Return Type**: `[number, number]`
- **Calls**:
  - `node.getStart`
  - `node.getEnd`
### `isToken(node: ts.Node): node is ts.Token<ts.TokenSyntaxKind>`

<details><summary>Code</summary>

```ts
function isToken(node: ts.Node): node is ts.Token<ts.TokenSyntaxKind> {
  return (
    node.kind >= SyntaxKind.FirstToken && node.kind <= SyntaxKind.LastToken
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if a given ts.Node is a token
 */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `node is ts.Token<ts.TokenSyntaxKind>`
### `isJSXToken(node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
export function isJSXToken(node: ts.Node): boolean {
  return (
    node.kind >= SyntaxKind.JsxElement && node.kind <= SyntaxKind.JsxAttribute
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if a given ts.Node is a JSX token
 */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `boolean`
### `getDeclarationKind(node: ts.VariableDeclarationList): DeclarationKind`

<details><summary>Code</summary>

```ts
export function getDeclarationKind(
  node: ts.VariableDeclarationList,
): DeclarationKind {
  if (node.flags & ts.NodeFlags.Let) {
    return 'let';
  }
  // eslint-disable-next-line @typescript-eslint/no-unsafe-enum-comparison
  if ((node.flags & ts.NodeFlags.AwaitUsing) === ts.NodeFlags.AwaitUsing) {
    return 'await using';
  }
  if (node.flags & ts.NodeFlags.Const) {
    return 'const';
  }
  if (node.flags & ts.NodeFlags.Using) {
    return 'using';
  }
  return 'var';
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns the declaration kind of the given ts.Node
 */
```

- **Parameters**:
  - `node: ts.VariableDeclarationList`
- **Return Type**: `DeclarationKind`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-unsafe-enum-comparison
```

### `getTSNodeAccessibility(node: ts.Node): 'private' | 'protected' | 'public' | undefined`

<details><summary>Code</summary>

```ts
export function getTSNodeAccessibility(
  node: ts.Node,
): 'private' | 'protected' | 'public' | undefined {
  const modifiers = getModifiers(node);
  if (modifiers == null) {
    return undefined;
  }
  for (const modifier of modifiers) {
    switch (modifier.kind) {
      case SyntaxKind.PublicKeyword:
        return 'public';
      case SyntaxKind.ProtectedKeyword:
        return 'protected';
      case SyntaxKind.PrivateKeyword:
        return 'private';
      default:
        break;
    }
  }
  return undefined;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets a ts.Node's accessibility level
 */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `'private' | 'protected' | 'public' | undefined`
- **Calls**:
  - `getModifiers (from ./getModifiers)`
### `findNextToken(previousToken: ts.TextRange, parent: ts.Node, ast: ts.SourceFile): ts.Node | undefined`

<details><summary>Code</summary>

```ts
export function findNextToken(
  previousToken: ts.TextRange,
  parent: ts.Node,
  ast: ts.SourceFile,
): ts.Node | undefined {
  return find(parent);

  function find(n: ts.Node): ts.Node | undefined {
    if (ts.isToken(n) && n.pos === previousToken.end) {
      // this is token that starts at the end of previous token - return it
      return n;
    }
    return firstDefined(n.getChildren(ast), (child: ts.Node) => {
      const shouldDiveInChildNode =
        // previous token is enclosed somewhere in the child
        (child.pos <= previousToken.pos && child.end > previousToken.end) ||
        // previous token ends exactly at the beginning of child
        child.pos === previousToken.end;
      return shouldDiveInChildNode && nodeHasTokens(child, ast)
        ? find(child)
        : undefined;
    });
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Finds the next token based on the previous one and its parent
 * Had to copy this from TS instead of using TS's version because theirs doesn't pass the ast to getChildren
 */
```

- **Parameters**:
  - `previousToken: ts.TextRange`
  - `parent: ts.Node`
  - `ast: ts.SourceFile`
- **Return Type**: `ts.Node | undefined`
- **Calls**:
  - `find`
  - `ts.isToken`
  - `firstDefined`
  - `n.getChildren`
  - `nodeHasTokens`
- **Internal Comments**:
```
// this is token that starts at the end of previous token - return it
// previous token is enclosed somewhere in the child (x2)
// previous token ends exactly at the beginning of child (x3)
```

### `find(n: ts.Node): ts.Node | undefined`

<details><summary>Code</summary>

```ts
function find(n: ts.Node): ts.Node | undefined {
    if (ts.isToken(n) && n.pos === previousToken.end) {
      // this is token that starts at the end of previous token - return it
      return n;
    }
    return firstDefined(n.getChildren(ast), (child: ts.Node) => {
      const shouldDiveInChildNode =
        // previous token is enclosed somewhere in the child
        (child.pos <= previousToken.pos && child.end > previousToken.end) ||
        // previous token ends exactly at the beginning of child
        child.pos === previousToken.end;
      return shouldDiveInChildNode && nodeHasTokens(child, ast)
        ? find(child)
        : undefined;
    });
  }
```
</details>

- **Parameters**:
  - `n: ts.Node`
- **Return Type**: `ts.Node | undefined`
- **Calls**:
  - `ts.isToken`
  - `firstDefined`
  - `n.getChildren`
  - `nodeHasTokens`
  - `find`
- **Internal Comments**:
```
// this is token that starts at the end of previous token - return it
// previous token is enclosed somewhere in the child (x2)
// previous token ends exactly at the beginning of child (x3)
```

### `findFirstMatchingAncestor(node: ts.Node, predicate: (node: ts.Node) => boolean): ts.Node | undefined`

<details><summary>Code</summary>

```ts
export function findFirstMatchingAncestor(
  node: ts.Node,
  predicate: (node: ts.Node) => boolean,
): ts.Node | undefined {
  let current: ts.Node | undefined = node;
  while (current) {
    if (predicate(current)) {
      return current;
    }
    current = current.parent as ts.Node | undefined;
  }
  return undefined;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Find the first matching ancestor based on the given predicate function.
 * @param node The current ts.Node
 * @param predicate The predicate function to apply to each checked ancestor
 * @returns a matching parent ts.Node
 */
```

- **Parameters**:
  - `node: ts.Node`
  - `predicate: (node: ts.Node) => boolean`
- **Return Type**: `ts.Node | undefined`
- **Calls**:
  - `predicate`
### `hasJSXAncestor(node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
export function hasJSXAncestor(node: ts.Node): boolean {
  return !!findFirstMatchingAncestor(node, isJSXToken);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if a given ts.Node has a JSX token within its hierarchy
 */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `findFirstMatchingAncestor`
### `unescapeStringLiteralText(text: string): string`

<details><summary>Code</summary>

```ts
export function unescapeStringLiteralText(text: string): string {
  return text.replaceAll(/&(?:#\d+|#x[\da-fA-F]+|[0-9a-zA-Z]+);/g, entity => {
    const item = entity.slice(1, -1);
    if (item[0] === '#') {
      const codePoint =
        item[1] === 'x'
          ? parseInt(item.slice(2), 16)
          : parseInt(item.slice(1), 10);
      return codePoint > 0x10ffff // RangeError: Invalid code point
        ? entity
        : String.fromCodePoint(codePoint);
    }
    return xhtmlEntities[item] || entity;
  });
}
```
</details>

- **JSDoc**:
```ts
/**
 * Unescape the text content of string literals, e.g. &amp; -> &
 * @param text The escaped string literal text.
 * @returns The unescaped string literal text.
 */
```

- **Parameters**:
  - `text: string`
- **Return Type**: `string`
- **Calls**:
  - `text.replaceAll`
  - `entity.slice`
  - `parseInt`
  - `item.slice`
  - `String.fromCodePoint`
### `isComputedProperty(node: ts.Node): node is ts.ComputedPropertyName`

<details><summary>Code</summary>

```ts
export function isComputedProperty(
  node: ts.Node,
): node is ts.ComputedPropertyName {
  return node.kind === SyntaxKind.ComputedPropertyName;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if a given ts.Node is a computed property
 */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `node is ts.ComputedPropertyName`
### `isOptional(node: {
  questionToken?: ts.QuestionToken;
}): boolean`

<details><summary>Code</summary>

```ts
export function isOptional(node: {
  questionToken?: ts.QuestionToken;
}): boolean {
  return !!node.questionToken;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if a given ts.Node is optional (has QuestionToken)
 * @param node ts.Node to be checked
 */
```

- **Parameters**:
  - `node: {
  questionToken?: ts.QuestionToken;
}`
- **Return Type**: `boolean`
### `isChainExpression(node: TSESTree.Node): node is TSESTree.ChainExpression`

<details><summary>Code</summary>

```ts
export function isChainExpression(
  node: TSESTree.Node,
): node is TSESTree.ChainExpression {
  return node.type === AST_NODE_TYPES.ChainExpression;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if the node is an optional chain node
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.ChainExpression`
### `isChildUnwrappableOptionalChain(node: | ts.CallExpression
    | ts.ElementAccessExpression
    | ts.NonNullExpression
    | ts.PropertyAccessExpression, child: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
export function isChildUnwrappableOptionalChain(
  node:
    | ts.CallExpression
    | ts.ElementAccessExpression
    | ts.NonNullExpression
    | ts.PropertyAccessExpression,
  child: TSESTree.Node,
): boolean {
  return (
    isChainExpression(child) &&
    // (x?.y).z is semantically different, and as such .z is no longer optional
    node.expression.kind !== ts.SyntaxKind.ParenthesizedExpression
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true of the child of property access expression is an optional chain
 */
```

- **Parameters**:
  - `node: | ts.CallExpression
    | ts.ElementAccessExpression
    | ts.NonNullExpression
    | ts.PropertyAccessExpression`
  - `child: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isChainExpression`
- **Internal Comments**:
```
// (x?.y).z is semantically different, and as such .z is no longer optional (x4)
```

### `getTokenType(token: ts.Identifier | ts.Token<ts.SyntaxKind>): Exclude<AST_TOKEN_TYPES, AST_TOKEN_TYPES.Block | AST_TOKEN_TYPES.Line>`

<details><summary>Code</summary>

```ts
export function getTokenType(
  token: ts.Identifier | ts.Token<ts.SyntaxKind>,
): Exclude<AST_TOKEN_TYPES, AST_TOKEN_TYPES.Block | AST_TOKEN_TYPES.Line> {
  let keywordKind: ts.SyntaxKind | undefined;
  if (isAtLeast50 && token.kind === SyntaxKind.Identifier) {
    keywordKind = ts.identifierToKeywordKind(token as ts.Identifier);
  } else if ('originalKeywordKind' in token) {
    // @ts-expect-error -- intentional fallback for older TS versions <=4.9
    keywordKind = token.originalKeywordKind;
  }
  if (keywordKind) {
    if (keywordKind === SyntaxKind.NullKeyword) {
      return AST_TOKEN_TYPES.Null;
    }
    if (
      keywordKind >= SyntaxKind.FirstFutureReservedWord &&
      keywordKind <= SyntaxKind.LastKeyword
    ) {
      return AST_TOKEN_TYPES.Identifier;
    }
    return AST_TOKEN_TYPES.Keyword;
  }

  if (
    token.kind >= SyntaxKind.FirstKeyword &&
    token.kind <= SyntaxKind.LastFutureReservedWord
  ) {
    if (
      token.kind === SyntaxKind.FalseKeyword ||
      token.kind === SyntaxKind.TrueKeyword
    ) {
      return AST_TOKEN_TYPES.Boolean;
    }

    return AST_TOKEN_TYPES.Keyword;
  }

  if (
    token.kind >= SyntaxKind.FirstPunctuation &&
    token.kind <= SyntaxKind.LastPunctuation
  ) {
    return AST_TOKEN_TYPES.Punctuator;
  }

  if (
    token.kind >= SyntaxKind.NoSubstitutionTemplateLiteral &&
    token.kind <= SyntaxKind.TemplateTail
  ) {
    return AST_TOKEN_TYPES.Template;
  }

  switch (token.kind) {
    case SyntaxKind.NumericLiteral:
    case SyntaxKind.BigIntLiteral:
      return AST_TOKEN_TYPES.Numeric;

    case SyntaxKind.PrivateIdentifier:
      return AST_TOKEN_TYPES.PrivateIdentifier;

    case SyntaxKind.JsxText:
      return AST_TOKEN_TYPES.JSXText;

    case SyntaxKind.StringLiteral:
      // A TypeScript-StringLiteral token with a TypeScript-JsxAttribute or TypeScript-JsxElement parent,
      // must actually be an ESTree-JSXText token
      if (
        token.parent.kind === SyntaxKind.JsxAttribute ||
        token.parent.kind === SyntaxKind.JsxElement
      ) {
        return AST_TOKEN_TYPES.JSXText;
      }

      return AST_TOKEN_TYPES.String;

    case SyntaxKind.RegularExpressionLiteral:
      return AST_TOKEN_TYPES.RegularExpression;

    case SyntaxKind.Identifier:
    case SyntaxKind.ConstructorKeyword:
    case SyntaxKind.GetKeyword:
    case SyntaxKind.SetKeyword:

    // intentional fallthrough
    default:
  }

  // Some JSX tokens have to be determined based on their parent
  if (token.kind === SyntaxKind.Identifier) {
    if (isJSXToken(token.parent)) {
      return AST_TOKEN_TYPES.JSXIdentifier;
    }

    if (
      token.parent.kind === SyntaxKind.PropertyAccessExpression &&
      hasJSXAncestor(token)
    ) {
      return AST_TOKEN_TYPES.JSXIdentifier;
    }
  }

  return AST_TOKEN_TYPES.Identifier;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns the type of a given ts.Token
 */
```

- **Parameters**:
  - `token: ts.Identifier | ts.Token<ts.SyntaxKind>`
- **Return Type**: `Exclude<AST_TOKEN_TYPES, AST_TOKEN_TYPES.Block | AST_TOKEN_TYPES.Line>`
- **Calls**:
  - `ts.identifierToKeywordKind`
  - `isJSXToken`
  - `hasJSXAncestor`
- **Internal Comments**:
```
// @ts-expect-error -- intentional fallback for older TS versions <=4.9 (x3)
// A TypeScript-StringLiteral token with a TypeScript-JsxAttribute or TypeScript-JsxElement parent,
// must actually be an ESTree-JSXText token
// intentional fallthrough
// Some JSX tokens have to be determined based on their parent
```

### `convertToken(token: ts.Token<ts.TokenSyntaxKind>, ast: ts.SourceFile): TSESTree.Token`

<details><summary>Code</summary>

```ts
export function convertToken(
  token: ts.Token<ts.TokenSyntaxKind>,
  ast: ts.SourceFile,
): TSESTree.Token {
  const start =
    token.kind === SyntaxKind.JsxText
      ? token.getFullStart()
      : token.getStart(ast);
  const end = token.getEnd();
  const value = ast.text.slice(start, end);
  const tokenType = getTokenType(token);
  const range: TSESTree.Range = [start, end];
  const loc = getLocFor(range, ast);

  if (tokenType === AST_TOKEN_TYPES.RegularExpression) {
    return {
      type: tokenType,
      loc,
      range,
      regex: {
        flags: value.slice(value.lastIndexOf('/') + 1),
        pattern: value.slice(1, value.lastIndexOf('/')),
      },
      value,
    };
  }

  if (tokenType === AST_TOKEN_TYPES.PrivateIdentifier) {
    return {
      type: tokenType,
      loc,
      range,
      value: value.slice(1),
    };
  }

  // @ts-expect-error TS is complaining about `value` not being the correct
  // type but it is
  return {
    type: tokenType,
    loc,
    range,
    value,
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Extends and formats a given ts.Token, for a given AST
 */
```

- **Parameters**:
  - `token: ts.Token<ts.TokenSyntaxKind>`
  - `ast: ts.SourceFile`
- **Return Type**: `TSESTree.Token`
- **Calls**:
  - `token.getFullStart`
  - `token.getStart`
  - `token.getEnd`
  - `ast.text.slice`
  - `getTokenType`
  - `getLocFor`
  - `value.slice`
  - `value.lastIndexOf`
- **Internal Comments**:
```
// @ts-expect-error TS is complaining about `value` not being the correct
// type but it is
```

### `convertTokens(ast: ts.SourceFile): TSESTree.Token[]`

<details><summary>Code</summary>

```ts
export function convertTokens(ast: ts.SourceFile): TSESTree.Token[] {
  const result: TSESTree.Token[] = [];
  /**
   * @param node the ts.Node
   */
  function walk(node: ts.Node): void {
    // TypeScript generates tokens for types in JSDoc blocks. Comment tokens
    // and their children should not be walked or added to the resulting tokens list.
    if (isComment(node) || isJSDocComment(node)) {
      return;
    }

    if (isToken(node) && node.kind !== SyntaxKind.EndOfFileToken) {
      result.push(convertToken(node, ast));
    } else {
      node.getChildren(ast).forEach(walk);
    }
  }
  walk(ast);
  return result;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Converts all tokens for the given AST
 * @param ast the AST object
 * @returns the converted Tokens
 */
```

- **Parameters**:
  - `ast: ts.SourceFile`
- **Return Type**: `TSESTree.Token[]`
- **Calls**:
  - `isComment`
  - `isJSDocComment`
  - `isToken`
  - `result.push`
  - `convertToken`
  - `node.getChildren(ast).forEach`
  - `walk`
- **Internal Comments**:
```
/**
   * @param node the ts.Node
   */
// TypeScript generates tokens for types in JSDoc blocks. Comment tokens
// and their children should not be walked or added to the resulting tokens list.
```

### `walk(node: ts.Node): void`

<details><summary>Code</summary>

```ts
function walk(node: ts.Node): void {
    // TypeScript generates tokens for types in JSDoc blocks. Comment tokens
    // and their children should not be walked or added to the resulting tokens list.
    if (isComment(node) || isJSDocComment(node)) {
      return;
    }

    if (isToken(node) && node.kind !== SyntaxKind.EndOfFileToken) {
      result.push(convertToken(node, ast));
    } else {
      node.getChildren(ast).forEach(walk);
    }
  }
```
</details>

- **JSDoc**:
```ts
/**
   * @param node the ts.Node
   */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `void`
- **Calls**:
  - `isComment`
  - `isJSDocComment`
  - `isToken`
  - `result.push`
  - `convertToken`
  - `node.getChildren(ast).forEach`
- **Internal Comments**:
```
// TypeScript generates tokens for types in JSDoc blocks. Comment tokens
// and their children should not be walked or added to the resulting tokens list.
```

### `createError(message: string, ast: ts.SourceFile, startIndex: number, endIndex: number): TSError`

<details><summary>Code</summary>

```ts
export function createError(
  message: string,
  ast: ts.SourceFile,
  startIndex: number,
  endIndex: number = startIndex,
): TSError {
  const [start, end] = [startIndex, endIndex].map(offset => {
    const { character: column, line } =
      ast.getLineAndCharacterOfPosition(offset);
    return { column, line: line + 1, offset };
  });
  return new TSError(message, ast.fileName, { end, start });
}
```
</details>

- **Parameters**:
  - `message: string`
  - `ast: ts.SourceFile`
  - `startIndex: number`
  - `endIndex: number`
- **Return Type**: `TSError`
- **Calls**:
  - `[startIndex, endIndex].map`
  - `ast.getLineAndCharacterOfPosition`
### `nodeHasIllegalDecorators(node: ts.Node): node is { illegalDecorators: ts.Node[] } & ts.Node`

<details><summary>Code</summary>

```ts
export function nodeHasIllegalDecorators(
  node: ts.Node,
): node is { illegalDecorators: ts.Node[] } & ts.Node {
  return !!(
    'illegalDecorators' in node &&
    (node.illegalDecorators as unknown[] | undefined)?.length
  );
}
```
</details>

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `node is { illegalDecorators: ts.Node[] } & ts.Node`
### `nodeHasTokens(n: ts.Node, ast: ts.SourceFile): boolean`

<details><summary>Code</summary>

```ts
export function nodeHasTokens(n: ts.Node, ast: ts.SourceFile): boolean {
  // If we have a token or node that has a non-zero width, it must have tokens.
  // Note: getWidth() does not take trivia into account.
  return n.kind === SyntaxKind.EndOfFileToken
    ? !!(n as ts.JSDocContainer).jsDoc
    : n.getWidth(ast) !== 0;
}
```
</details>

- **Parameters**:
  - `n: ts.Node`
  - `ast: ts.SourceFile`
- **Return Type**: `boolean`
- **Calls**:
  - `n.getWidth`
- **Internal Comments**:
```
// If we have a token or node that has a non-zero width, it must have tokens.
// Note: getWidth() does not take trivia into account.
```

### `firstDefined(array: readonly T[] | undefined, callback: (element: T, index: number) => U | undefined): U | undefined`

<details><summary>Code</summary>

```ts
export function firstDefined<T, U>(
  array: readonly T[] | undefined,
  callback: (element: T, index: number) => U | undefined,
): U | undefined {
  // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
  if (array === undefined) {
    return undefined;
  }

  for (let i = 0; i < array.length; i++) {
    const result = callback(array[i], i);
    // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
    if (result !== undefined) {
      return result;
    }
  }
  return undefined;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Like `forEach`, but suitable for use with numbers and strings (which may be falsy).
 */
```

- **Parameters**:
  - `array: readonly T[] | undefined`
  - `callback: (element: T, index: number) => U | undefined`
- **Return Type**: `U | undefined`
- **Calls**:
  - `callback`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish (x2)
```

### `identifierIsThisKeyword(id: ts.Identifier): boolean`

<details><summary>Code</summary>

```ts
export function identifierIsThisKeyword(id: ts.Identifier): boolean {
  return (
    (isAtLeast50
      ? ts.identifierToKeywordKind(id)
      : // @ts-expect-error -- intentional fallback for older TS versions <=4.9
        id.originalKeywordKind) === SyntaxKind.ThisKeyword
  );
}
```
</details>

- **Parameters**:
  - `id: ts.Identifier`
- **Return Type**: `boolean`
- **Calls**:
  - `ts.identifierToKeywordKind`
### `isThisIdentifier(node: ts.Node | undefined): node is ts.Identifier`

<details><summary>Code</summary>

```ts
export function isThisIdentifier(
  node: ts.Node | undefined,
): node is ts.Identifier {
  return (
    !!node &&
    node.kind === SyntaxKind.Identifier &&
    identifierIsThisKeyword(node as ts.Identifier)
  );
}
```
</details>

- **Parameters**:
  - `node: ts.Node | undefined`
- **Return Type**: `node is ts.Identifier`
- **Calls**:
  - `identifierIsThisKeyword`
### `isThisInTypeQuery(node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
export function isThisInTypeQuery(node: ts.Node): boolean {
  if (!isThisIdentifier(node)) {
    return false;
  }

  while (ts.isQualifiedName(node.parent) && node.parent.left === node) {
    node = node.parent;
  }

  return node.parent.kind === SyntaxKind.TypeQuery;
}
```
</details>

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isThisIdentifier`
  - `ts.isQualifiedName`
### `nodeIsMissing(node: ts.Node | undefined): boolean`

<details><summary>Code</summary>

```ts
function nodeIsMissing(node: ts.Node | undefined): boolean {
  if (node == null) {
    return true;
  }
  return (
    node.pos === node.end &&
    node.pos >= 0 &&
    node.kind !== SyntaxKind.EndOfFileToken
  );
}
```
</details>

- **Parameters**:
  - `node: ts.Node | undefined`
- **Return Type**: `boolean`
### `nodeIsPresent(node: ts.Node | undefined): node is ts.Node`

<details><summary>Code</summary>

```ts
export function nodeIsPresent(node: ts.Node | undefined): node is ts.Node {
  return !nodeIsMissing(node);
}
```
</details>

- **Parameters**:
  - `node: ts.Node | undefined`
- **Return Type**: `node is ts.Node`
- **Calls**:
  - `nodeIsMissing`
### `getContainingFunction(node: ts.Node): ts.SignatureDeclaration | undefined`

<details><summary>Code</summary>

```ts
export function getContainingFunction(
  node: ts.Node,
): ts.SignatureDeclaration | undefined {
  return ts.findAncestor(node.parent, ts.isFunctionLike);
}
```
</details>

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `ts.SignatureDeclaration | undefined`
- **Calls**:
  - `ts.findAncestor`
### `hasAbstractModifier(node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
function hasAbstractModifier(node: ts.Node): boolean {
  return hasModifier(SyntaxKind.AbstractKeyword, node);
}
```
</details>

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `hasModifier`
### `getThisParameter(signature: ts.SignatureDeclaration): ts.ParameterDeclaration | null`

<details><summary>Code</summary>

```ts
function getThisParameter(
  signature: ts.SignatureDeclaration,
): ts.ParameterDeclaration | null {
  if (signature.parameters.length && !ts.isJSDocSignature(signature)) {
    const thisParameter = signature.parameters[0];
    if (parameterIsThisKeyword(thisParameter)) {
      return thisParameter;
    }
  }

  return null;
}
```
</details>

- **Parameters**:
  - `signature: ts.SignatureDeclaration`
- **Return Type**: `ts.ParameterDeclaration | null`
- **Calls**:
  - `ts.isJSDocSignature`
  - `parameterIsThisKeyword`
### `parameterIsThisKeyword(parameter: ts.ParameterDeclaration): boolean`

<details><summary>Code</summary>

```ts
function parameterIsThisKeyword(parameter: ts.ParameterDeclaration): boolean {
  return isThisIdentifier(parameter.name);
}
```
</details>

- **Parameters**:
  - `parameter: ts.ParameterDeclaration`
- **Return Type**: `boolean`
- **Calls**:
  - `isThisIdentifier`
### `nodeCanBeDecorated(node: TSNode): boolean`

<details><summary>Code</summary>

```ts
export function nodeCanBeDecorated(node: TSNode): boolean {
  switch (node.kind) {
    case SyntaxKind.ClassDeclaration:
      return true;
    case SyntaxKind.ClassExpression:
      // `ts.nodeCanBeDecorated` returns `false` if `useLegacyDecorators: true`
      return true;
    case SyntaxKind.PropertyDeclaration: {
      const { parent } = node;

      // `ts.nodeCanBeDecorated` uses this if `useLegacyDecorators: true`
      if (ts.isClassDeclaration(parent)) {
        return true;
      }

      // `ts.nodeCanBeDecorated` uses this if `useLegacyDecorators: false`
      if (ts.isClassLike(parent) && !hasAbstractModifier(node)) {
        return true;
      }

      return false;
    }
    case SyntaxKind.GetAccessor:
    case SyntaxKind.SetAccessor:
    case SyntaxKind.MethodDeclaration: {
      const { parent } = node;
      // In `ts.nodeCanBeDecorated`
      // when `useLegacyDecorators: true` uses `ts.isClassDeclaration`
      // when `useLegacyDecorators: true` uses `ts.isClassLike`
      return (
        Boolean(node.body) &&
        (ts.isClassDeclaration(parent) || ts.isClassLike(parent))
      );
    }
    case SyntaxKind.Parameter: {
      // `ts.nodeCanBeDecorated` returns `false` if `useLegacyDecorators: false`

      const { parent } = node;
      const grandparent = parent.parent;

      return (
        Boolean(parent) &&
        'body' in parent &&
        Boolean(parent.body) &&
        (parent.kind === SyntaxKind.Constructor ||
          parent.kind === SyntaxKind.MethodDeclaration ||
          parent.kind === SyntaxKind.SetAccessor) &&
        getThisParameter(parent) !== node &&
        Boolean(grandparent) &&
        grandparent.kind === SyntaxKind.ClassDeclaration
      );
    }
  }

  return false;
}
```
</details>

- **Parameters**:
  - `node: TSNode`
- **Return Type**: `boolean`
- **Calls**:
  - `ts.isClassDeclaration`
  - `ts.isClassLike`
  - `hasAbstractModifier`
  - `Boolean`
  - `getThisParameter`
- **Internal Comments**:
```
// `ts.nodeCanBeDecorated` returns `false` if `useLegacyDecorators: true`
// `ts.nodeCanBeDecorated` uses this if `useLegacyDecorators: true`
// `ts.nodeCanBeDecorated` uses this if `useLegacyDecorators: false`
// In `ts.nodeCanBeDecorated`
// when `useLegacyDecorators: true` uses `ts.isClassDeclaration`
// when `useLegacyDecorators: true` uses `ts.isClassLike`
// `ts.nodeCanBeDecorated` returns `false` if `useLegacyDecorators: false` (x2)
```

### `isValidAssignmentTarget(node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
export function isValidAssignmentTarget(node: ts.Node): boolean {
  switch (node.kind) {
    case SyntaxKind.Identifier:
      return true;
    case SyntaxKind.PropertyAccessExpression:
    case SyntaxKind.ElementAccessExpression:
      if (node.flags & ts.NodeFlags.OptionalChain) {
        return false;
      }
      return true;
    case SyntaxKind.ParenthesizedExpression:
    case SyntaxKind.TypeAssertionExpression:
    case SyntaxKind.AsExpression:
    case SyntaxKind.SatisfiesExpression:
    case SyntaxKind.ExpressionWithTypeArguments:
    case SyntaxKind.NonNullExpression:
      return isValidAssignmentTarget(
        (
          node as
            | ts.AssertionExpression
            | ts.ExpressionWithTypeArguments
            | ts.NonNullExpression
            | ts.ParenthesizedExpression
            | ts.SatisfiesExpression
        ).expression,
      );
    default:
      return false;
  }
}
```
</details>

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isValidAssignmentTarget`
### `getNamespaceModifiers(node: ts.ModuleDeclaration): ts.Modifier[] | undefined`

<details><summary>Code</summary>

```ts
export function getNamespaceModifiers(
  node: ts.ModuleDeclaration,
): ts.Modifier[] | undefined {
  // For following nested namespaces, use modifiers given to the topmost namespace
  //   export declare namespace foo.bar.baz {}
  let modifiers = getModifiers(node);
  let moduleDeclaration = node;
  while (
    (!modifiers || modifiers.length === 0) &&
    ts.isModuleDeclaration(moduleDeclaration.parent)
  ) {
    const parentModifiers = getModifiers(moduleDeclaration.parent);
    if (parentModifiers?.length) {
      modifiers = parentModifiers;
    }
    moduleDeclaration = moduleDeclaration.parent;
  }
  return modifiers;
}
```
</details>

- **Parameters**:
  - `node: ts.ModuleDeclaration`
- **Return Type**: `ts.Modifier[] | undefined`
- **Calls**:
  - `getModifiers (from ./getModifiers)`
  - `ts.isModuleDeclaration`
- **Internal Comments**:
```
// For following nested namespaces, use modifiers given to the topmost namespace (x2)
//   export declare namespace foo.bar.baz {} (x2)
```


---

## Classes

### `TSError`

<details><summary>Class Code</summary>

```ts
export class TSError extends Error {
  constructor(
    message: string,
    public readonly fileName: string,
    public readonly location: {
      end: {
        column: number;
        line: number;
        offset: number;
      };
      start: {
        column: number;
        line: number;
        offset: number;
      };
    },
  ) {
    super(message);
    Object.defineProperty(this, 'name', {
      configurable: true,
      enumerable: false,
      value: new.target.name,
    });
  }

  // For old version of ESLint https://github.com/typescript-eslint/typescript-eslint/pull/6556#discussion_r1123237311
  get index(): number {
    return this.location.start.offset;
  }

  // https://github.com/eslint/eslint/blob/b09a512107249a4eb19ef5a37b0bd672266eafdb/lib/linter/linter.js#L853
  get lineNumber(): number {
    return this.location.start.line;
  }

  // https://github.com/eslint/eslint/blob/b09a512107249a4eb19ef5a37b0bd672266eafdb/lib/linter/linter.js#L854
  get column(): number {
    return this.location.start.column;
  }
}
```
</details>


---

## Interfaces

### `TokenToText`

<details><summary>Interface Code</summary>

```ts
interface TokenToText
  extends TSESTree.PunctuatorTokenToText,
    TSESTree.BinaryOperatorToText {
  [SyntaxKind.ImportKeyword]: 'import';
  [SyntaxKind.KeyOfKeyword]: 'keyof';
  [SyntaxKind.NewKeyword]: 'new';
  [SyntaxKind.ReadonlyKeyword]: 'readonly';
  [SyntaxKind.UniqueKeyword]: 'unique';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `[SyntaxKind.ImportKeyword]` | `'import'` | ✗ |  |
| `[SyntaxKind.KeyOfKeyword]` | `'keyof'` | ✗ |  |
| `[SyntaxKind.NewKeyword]` | `'new'` | ✗ |  |
| `[SyntaxKind.ReadonlyKeyword]` | `'readonly'` | ✗ |  |
| `[SyntaxKind.UniqueKeyword]` | `'unique'` | ✗ |  |


---

## Type Aliases

### `LogicalOperatorKind`

```ts
type LogicalOperatorKind = | ts.SyntaxKind.AmpersandAmpersandToken
  | ts.SyntaxKind.BarBarToken
  | ts.SyntaxKind.QuestionQuestionToken;
```

### `AssignmentOperatorKind`

```ts
type AssignmentOperatorKind = keyof TSESTree.AssignmentOperatorToText;
```

### `BinaryOperatorKind`

```ts
type BinaryOperatorKind = keyof TSESTree.BinaryOperatorToText;
```

### `DeclarationKind`

```ts
type DeclarationKind = TSESTree.VariableDeclaration['kind'];
```

### `TokenForTokenKind<T extends ts.SyntaxKind extends ts.SyntaxKind>`

```ts
type TokenForTokenKind<T extends ts.SyntaxKind extends ts.SyntaxKind> = T extends keyof TokenToText
  ? TokenToText[T]
  : string | undefined;
```


---