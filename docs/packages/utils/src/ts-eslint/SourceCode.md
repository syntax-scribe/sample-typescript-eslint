[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `SourceCode.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 36 |
| 🧱 Classes | 3 |
| 📦 Imports | 5 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 7 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/utils/src/ts-eslint/SourceCode.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintSourceCode` | `eslint` |
| `ParserServices` | `../ts-estree` |
| `TSESTree` | `../ts-estree` |
| `Parser` | `./Parser` |
| `Scope` | `./Scope` |


---

## Functions

### `TokenStore.commentsExistBetween(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token): boolean`

<details><summary>Code</summary>

```ts
commentsExistBetween(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
  ): boolean;
```
</details>

- **JSDoc**:
```ts
/**
   * Checks whether any comments exist or not between the given 2 nodes.
   * @param left The node to check.
   * @param right The node to check.
   * @returns `true` if one or more comments exist.
   */
```

- **Parameters**:
  - `left: TSESTree.Node | TSESTree.Token`
  - `right: TSESTree.Node | TSESTree.Token`
- **Return Type**: `boolean`
### `TokenStore.getCommentsAfter(nodeOrToken: TSESTree.Node | TSESTree.Token): TSESTree.Comment[]`

<details><summary>Code</summary>

```ts
getCommentsAfter(
    nodeOrToken: TSESTree.Node | TSESTree.Token,
  ): TSESTree.Comment[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets all comment tokens directly after the given node or token.
   * @param nodeOrToken The AST node or token to check for adjacent comment tokens.
   * @returns An array of comments in occurrence order.
   */
```

- **Parameters**:
  - `nodeOrToken: TSESTree.Node | TSESTree.Token`
- **Return Type**: `TSESTree.Comment[]`
### `TokenStore.getCommentsBefore(nodeOrToken: TSESTree.Node | TSESTree.Token): TSESTree.Comment[]`

<details><summary>Code</summary>

```ts
getCommentsBefore(
    nodeOrToken: TSESTree.Node | TSESTree.Token,
  ): TSESTree.Comment[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets all comment tokens directly before the given node or token.
   * @param nodeOrToken The AST node or token to check for adjacent comment tokens.
   * @returns An array of comments in occurrence order.
   */
```

- **Parameters**:
  - `nodeOrToken: TSESTree.Node | TSESTree.Token`
- **Return Type**: `TSESTree.Comment[]`
### `TokenStore.getCommentsInside(node: TSESTree.Node): TSESTree.Comment[]`

<details><summary>Code</summary>

```ts
getCommentsInside(node: TSESTree.Node): TSESTree.Comment[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets all comment tokens inside the given node.
   * @param node The AST node to get the comments for.
   * @returns An array of comments in occurrence order.
   */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `TSESTree.Comment[]`
### `TokenStore.getFirstToken(node: TSESTree.Node, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getFirstToken<T extends SourceCode.CursorWithSkipOptions>(
    node: TSESTree.Node,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the first token of the given node.
   * @param node The AST node.
   * @param options The option object. If this is a number then it's `options.skip`. If this is a function then it's `options.filter`.
   * @returns An object representing the token.
   */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `options: T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T> | null`
### `TokenStore.getFirstTokenBetween(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getFirstTokenBetween<T extends SourceCode.CursorWithSkipOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the first token between two non-overlapping nodes.
   * @param left Node before the desired token range.
   * @param right Node after the desired token range.
   * @param options The option object. If this is a number then it's `options.skip`. If this is a function then it's `options.filter`.
   * @returns An object representing the token.
   */
```

- **Parameters**:
  - `left: TSESTree.Node | TSESTree.Token`
  - `right: TSESTree.Node | TSESTree.Token`
  - `options: T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T> | null`
### `TokenStore.getFirstTokens(node: TSESTree.Node, options: T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getFirstTokens<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the first `count` tokens of the given node.
   * @param node The AST node.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `options: T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T>[]`
### `TokenStore.getFirstTokensBetween(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token, options: T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getFirstTokensBetween<T extends SourceCode.CursorWithCountOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the first `count` tokens between two non-overlapping nodes.
   * @param left Node before the desired token range.
   * @param right Node after the desired token range.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   * @returns Tokens between left and right.
   */
```

- **Parameters**:
  - `left: TSESTree.Node | TSESTree.Token`
  - `right: TSESTree.Node | TSESTree.Token`
  - `options: T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T>[]`
### `TokenStore.getLastToken(node: TSESTree.Node, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getLastToken<T extends SourceCode.CursorWithSkipOptions>(
    node: TSESTree.Node,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the last token of the given node.
   * @param node The AST node.
   * @param options The option object. If this is a number then it's `options.skip`. If this is a function then it's `options.filter`.
   * @returns An object representing the token.
   */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `options: T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T> | null`
### `TokenStore.getLastTokenBetween(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getLastTokenBetween<T extends SourceCode.CursorWithSkipOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the last token between two non-overlapping nodes.
   * @param left Node before the desired token range.
   * @param right Node after the desired token range.
   * @param options The option object. If this is a number then it's `options.skip`. If this is a function then it's `options.filter`.
   * @returns An object representing the token.
   */
```

- **Parameters**:
  - `left: TSESTree.Node | TSESTree.Token`
  - `right: TSESTree.Node | TSESTree.Token`
  - `options: T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T> | null`
### `TokenStore.getLastTokens(node: TSESTree.Node, options: T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getLastTokens<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the last `count` tokens of the given node.
   * @param node The AST node.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `options: T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T>[]`
### `TokenStore.getLastTokensBetween(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token, options: T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getLastTokensBetween<T extends SourceCode.CursorWithCountOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the last `count` tokens between two non-overlapping nodes.
   * @param left Node before the desired token range.
   * @param right Node after the desired token range.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   * @returns Tokens between left and right.
   */
```

- **Parameters**:
  - `left: TSESTree.Node | TSESTree.Token`
  - `right: TSESTree.Node | TSESTree.Token`
  - `options: T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T>[]`
### `TokenStore.getTokenAfter(node: TSESTree.Node | TSESTree.Token, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getTokenAfter<T extends SourceCode.CursorWithSkipOptions>(
    node: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the token that follows a given node or token.
   * @param node The AST node or token.
   * @param options The option object. If this is a number then it's `options.skip`. If this is a function then it's `options.filter`.
   * @returns An object representing the token.
   */
```

- **Parameters**:
  - `node: TSESTree.Node | TSESTree.Token`
  - `options: T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T> | null`
### `TokenStore.getTokenBefore(node: TSESTree.Node | TSESTree.Token, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getTokenBefore<T extends SourceCode.CursorWithSkipOptions>(
    node: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the token that precedes a given node or token.
   * @param node The AST node or token.
   * @param options The option object
   * @returns An object representing the token.
   */
```

- **Parameters**:
  - `node: TSESTree.Node | TSESTree.Token`
  - `options: T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T> | null`
### `TokenStore.getTokenByRangeStart(offset: number, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getTokenByRangeStart<T extends { includeComments?: boolean }>(
    offset: number,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the token starting at the specified index.
   * @param offset Index of the start of the token's range.
   * @param options The option object. If this is a number then it's `options.skip`. If this is a function then it's `options.filter`.
   * @returns The token starting at index, or null if no such token.
   */
```

- **Parameters**:
  - `offset: number`
  - `options: T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T> | null`
### `TokenStore.getTokens(node: TSESTree.Node, beforeCount: number, afterCount: number): TSESTree.Token[]`

<details><summary>Code</summary>

```ts
getTokens(
    node: TSESTree.Node,
    beforeCount?: number,
    afterCount?: number,
  ): TSESTree.Token[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets all tokens that are related to the given node.
   * @param node The AST node.
   * @param beforeCount The number of tokens before the node to retrieve.
   * @param afterCount The number of tokens after the node to retrieve.
   * @returns Array of objects representing tokens.
   */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `beforeCount: number`
  - `afterCount: number`
- **Return Type**: `TSESTree.Token[]`
### `TokenStore.getTokens(node: TSESTree.Node, options: T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getTokens<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node,
    options: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets all tokens that are related to the given node.
   * @param node The AST node.
   * @param options The option object. If this is a function then it's `options.filter`.
   * @returns Array of objects representing tokens.
   */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `options: T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T>[]`
### `TokenStore.getTokensAfter(node: TSESTree.Node | TSESTree.Token, options: number | T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getTokensAfter<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node | TSESTree.Token,
    options?: number | T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the `count` tokens that follows a given node or token.
   * @param node The AST node.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   */
```

- **Parameters**:
  - `node: TSESTree.Node | TSESTree.Token`
  - `options: number | T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T>[]`
### `TokenStore.getTokensBefore(node: TSESTree.Node | TSESTree.Token, options: number | T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getTokensBefore<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node | TSESTree.Token,
    options?: number | T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the `count` tokens that precedes a given node or token.
   * @param node The AST node.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   */
```

- **Parameters**:
  - `node: TSESTree.Node | TSESTree.Token`
  - `options: number | T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T>[]`
### `TokenStore.getTokensBetween(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token, options: number | T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getTokensBetween<T extends SourceCode.CursorWithCountOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: number | T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets all of the tokens between two non-overlapping nodes.
   * @param left Node before the desired token range.
   * @param right Node after the desired token range.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   * @returns Tokens between left and right.
   */
```

- **Parameters**:
  - `left: TSESTree.Node | TSESTree.Token`
  - `right: TSESTree.Node | TSESTree.Token`
  - `options: number | T`
- **Return Type**: `SourceCode.ReturnTypeFromOptions<T>[]`
### `SourceCodeBase.applyInlineConfig(): void`

<details><summary>Code</summary>

```ts
applyInlineConfig(): void;
```
</details>

- **Return Type**: `void`
### `SourceCodeBase.applyLanguageOptions(): void`

<details><summary>Code</summary>

```ts
applyLanguageOptions(): void;
```
</details>

- **Return Type**: `void`
### `SourceCodeBase.finalize(): void`

<details><summary>Code</summary>

```ts
finalize(): void;
```
</details>

- **Return Type**: `void`
### `SourceCodeBase.getAllComments(): TSESTree.Comment[]`

<details><summary>Code</summary>

```ts
getAllComments(): TSESTree.Comment[];
```
</details>

- **JSDoc**:
```ts
/**
   * Retrieves an array containing all comments in the source code.
   * @returns An array of comment nodes.
   */
```

- **Return Type**: `TSESTree.Comment[]`
### `SourceCodeBase.getIndexFromLoc(location: TSESTree.Position): number`

<details><summary>Code</summary>

```ts
getIndexFromLoc(location: TSESTree.Position): number;
```
</details>

- **JSDoc**:
```ts
/**
   * Converts a (line, column) pair into a range index.
   * @param location A line/column location
   * @returns The range index of the location in the file.
   */
```

- **Parameters**:
  - `location: TSESTree.Position`
- **Return Type**: `number`
### `SourceCodeBase.getLines(): string[]`

<details><summary>Code</summary>

```ts
getLines(): string[];
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the entire source text split into an array of lines.
   * @returns The source text as an array of lines.
   */
```

- **Return Type**: `string[]`
### `SourceCodeBase.getLocFromIndex(index: number): TSESTree.Position`

<details><summary>Code</summary>

```ts
getLocFromIndex(index: number): TSESTree.Position;
```
</details>

- **JSDoc**:
```ts
/**
   * Converts a source text index into a (line, column) pair.
   * @param index The index of a character in a file
   * @returns A {line, column} location object with a 0-indexed column
   */
```

- **Parameters**:
  - `index: number`
- **Return Type**: `TSESTree.Position`
### `SourceCodeBase.getNodeByRangeIndex(index: number): TSESTree.Node | null`

<details><summary>Code</summary>

```ts
getNodeByRangeIndex(index: number): TSESTree.Node | null;
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the deepest node containing a range index.
   * @param index Range index of the desired node.
   * @returns The node if found or `null` if not found.
   */
```

- **Parameters**:
  - `index: number`
- **Return Type**: `TSESTree.Node | null`
### `SourceCodeBase.getText(node: TSESTree.Node | TSESTree.Token, beforeCount: number, afterCount: number): string`

<details><summary>Code</summary>

```ts
getText(
    node?: TSESTree.Node | TSESTree.Token,
    beforeCount?: number,
    afterCount?: number,
  ): string;
```
</details>

- **JSDoc**:
```ts
/**
   * Gets the source code for the given node.
   * @param node The AST node to get the text for.
   * @param beforeCount The number of characters before the node to retrieve.
   * @param afterCount The number of characters after the node to retrieve.
   * @returns The text representing the AST node.
   */
```

- **Parameters**:
  - `node: TSESTree.Node | TSESTree.Token`
  - `beforeCount: number`
  - `afterCount: number`
- **Return Type**: `string`
### `SourceCodeBase.isSpaceBetween(first: TSESTree.Node | TSESTree.Token, second: TSESTree.Node | TSESTree.Token): boolean`

<details><summary>Code</summary>

```ts
isSpaceBetween(
    first: TSESTree.Node | TSESTree.Token,
    second: TSESTree.Node | TSESTree.Token,
  ): boolean;
```
</details>

- **JSDoc**:
```ts
/**
   * Determines if two nodes or tokens have at least one whitespace character
   * between them. Order does not matter. Returns false if the given nodes or
   * tokens overlap.
   * @param first The first node or token to check between.
   * @param second The second node or token to check between.
   * @returns True if there is a whitespace character between any of the tokens found between the two given nodes or tokens.
   */
```

- **Parameters**:
  - `first: TSESTree.Node | TSESTree.Token`
  - `second: TSESTree.Node | TSESTree.Token`
- **Return Type**: `boolean`
### `SourceCodeBase.isSpaceBetweenTokens(first: TSESTree.Token, second: TSESTree.Token): boolean`

<details><summary>Code</summary>

```ts
isSpaceBetweenTokens(first: TSESTree.Token, second: TSESTree.Token): boolean;
```
</details>

- **JSDoc**:
```ts
/**
   * Determines if two nodes or tokens have at least one whitespace character
   * between them. Order does not matter. Returns false if the given nodes or
   * tokens overlap.
   * For backward compatibility, this method returns true if there are
   * `JSXText` tokens that contain whitespace between the two.
   * @param first The first node or token to check between.
   * @param second The second node or token to check between.
   * @returns {boolean} True if there is a whitespace character between
   * any of the tokens found between the two given nodes or tokens.
   * @deprecated in favor of isSpaceBetween
   */
```

- **Parameters**:
  - `first: TSESTree.Token`
  - `second: TSESTree.Token`
- **Return Type**: `boolean`
### `SourceCodeBase.getScope(node: TSESTree.Node): Scope.Scope`

<details><summary>Code</summary>

```ts
getScope(node: TSESTree.Node): Scope.Scope;
```
</details>

- **JSDoc**:
```ts
/**
   * Returns the scope of the given node.
   * This information can be used track references to variables.
   */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `Scope.Scope`
### `SourceCodeBase.getAncestors(node: TSESTree.Node): TSESTree.Node[]`

<details><summary>Code</summary>

```ts
getAncestors(node: TSESTree.Node): TSESTree.Node[];
```
</details>

- **JSDoc**:
```ts
/**
   * Returns an array of the ancestors of the given node, starting at
   * the root of the AST and continuing through the direct parent of the current node.
   * This array does not include the currently-traversed node itself.
   */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `TSESTree.Node[]`
### `SourceCodeBase.getDeclaredVariables(node: TSESTree.Node): readonly Scope.Variable[]`

<details><summary>Code</summary>

```ts
getDeclaredVariables(node: TSESTree.Node): readonly Scope.Variable[];
```
</details>

- **JSDoc**:
```ts
/**
   * Returns a list of variables declared by the given node.
   * This information can be used to track references to variables.
   */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `readonly Scope.Variable[]`
### `SourceCodeBase.markVariableAsUsed(name: string, node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
markVariableAsUsed(name: string, node: TSESTree.Node): boolean;
```
</details>

- **JSDoc**:
```ts
/**
   * Marks a variable with the given name in the current scope as used.
   * This affects the no-unused-vars rule.
   */
```

- **Parameters**:
  - `name: string`
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `SourceCodeBase.splitLines(text: string): string[]`

<details><summary>Code</summary>

```ts
static splitLines(text: string): string[];
```
</details>

- **JSDoc**:
```ts
/**
   * Split the source code into multiple lines based on the line delimiters.
   * @param text Source code as a string.
   * @returns Array of source code lines.
   */
```

- **Parameters**:
  - `text: string`
- **Return Type**: `string[]`

---

## Classes

### `TokenStore`

<details><summary>Class Code</summary>

```ts
declare class TokenStore {
  /**
   * Checks whether any comments exist or not between the given 2 nodes.
   * @param left The node to check.
   * @param right The node to check.
   * @returns `true` if one or more comments exist.
   */
  commentsExistBetween(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
  ): boolean;
  /**
   * Gets all comment tokens directly after the given node or token.
   * @param nodeOrToken The AST node or token to check for adjacent comment tokens.
   * @returns An array of comments in occurrence order.
   */
  getCommentsAfter(
    nodeOrToken: TSESTree.Node | TSESTree.Token,
  ): TSESTree.Comment[];
  /**
   * Gets all comment tokens directly before the given node or token.
   * @param nodeOrToken The AST node or token to check for adjacent comment tokens.
   * @returns An array of comments in occurrence order.
   */
  getCommentsBefore(
    nodeOrToken: TSESTree.Node | TSESTree.Token,
  ): TSESTree.Comment[];
  /**
   * Gets all comment tokens inside the given node.
   * @param node The AST node to get the comments for.
   * @returns An array of comments in occurrence order.
   */
  getCommentsInside(node: TSESTree.Node): TSESTree.Comment[];
  /**
   * Gets the first token of the given node.
   * @param node The AST node.
   * @param options The option object. If this is a number then it's `options.skip`. If this is a function then it's `options.filter`.
   * @returns An object representing the token.
   */
  getFirstToken<T extends SourceCode.CursorWithSkipOptions>(
    node: TSESTree.Node,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
  /**
   * Gets the first token between two non-overlapping nodes.
   * @param left Node before the desired token range.
   * @param right Node after the desired token range.
   * @param options The option object. If this is a number then it's `options.skip`. If this is a function then it's `options.filter`.
   * @returns An object representing the token.
   */
  getFirstTokenBetween<T extends SourceCode.CursorWithSkipOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
  /**
   * Gets the first `count` tokens of the given node.
   * @param node The AST node.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   */
  getFirstTokens<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
  /**
   * Gets the first `count` tokens between two non-overlapping nodes.
   * @param left Node before the desired token range.
   * @param right Node after the desired token range.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   * @returns Tokens between left and right.
   */
  getFirstTokensBetween<T extends SourceCode.CursorWithCountOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
  /**
   * Gets the last token of the given node.
   * @param node The AST node.
   * @param options The option object. If this is a number then it's `options.skip`. If this is a function then it's `options.filter`.
   * @returns An object representing the token.
   */
  getLastToken<T extends SourceCode.CursorWithSkipOptions>(
    node: TSESTree.Node,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
  /**
   * Gets the last token between two non-overlapping nodes.
   * @param left Node before the desired token range.
   * @param right Node after the desired token range.
   * @param options The option object. If this is a number then it's `options.skip`. If this is a function then it's `options.filter`.
   * @returns An object representing the token.
   */
  getLastTokenBetween<T extends SourceCode.CursorWithSkipOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
  /**
   * Gets the last `count` tokens of the given node.
   * @param node The AST node.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   */
  getLastTokens<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
  /**
   * Gets the last `count` tokens between two non-overlapping nodes.
   * @param left Node before the desired token range.
   * @param right Node after the desired token range.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   * @returns Tokens between left and right.
   */
  getLastTokensBetween<T extends SourceCode.CursorWithCountOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
  /**
   * Gets the token that follows a given node or token.
   * @param node The AST node or token.
   * @param options The option object. If this is a number then it's `options.skip`. If this is a function then it's `options.filter`.
   * @returns An object representing the token.
   */
  getTokenAfter<T extends SourceCode.CursorWithSkipOptions>(
    node: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
  /**
   * Gets the token that precedes a given node or token.
   * @param node The AST node or token.
   * @param options The option object
   * @returns An object representing the token.
   */
  getTokenBefore<T extends SourceCode.CursorWithSkipOptions>(
    node: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
  /**
   * Gets the token starting at the specified index.
   * @param offset Index of the start of the token's range.
   * @param options The option object. If this is a number then it's `options.skip`. If this is a function then it's `options.filter`.
   * @returns The token starting at index, or null if no such token.
   */
  getTokenByRangeStart<T extends { includeComments?: boolean }>(
    offset: number,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
  /**
   * Gets all tokens that are related to the given node.
   * @param node The AST node.
   * @param beforeCount The number of tokens before the node to retrieve.
   * @param afterCount The number of tokens after the node to retrieve.
   * @returns Array of objects representing tokens.
   */
  getTokens(
    node: TSESTree.Node,
    beforeCount?: number,
    afterCount?: number,
  ): TSESTree.Token[];
  /**
   * Gets all tokens that are related to the given node.
   * @param node The AST node.
   * @param options The option object. If this is a function then it's `options.filter`.
   * @returns Array of objects representing tokens.
   */
  getTokens<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node,
    options: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
  /**
   * Gets the `count` tokens that follows a given node or token.
   * @param node The AST node.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   */
  getTokensAfter<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node | TSESTree.Token,
    options?: number | T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
  /**
   * Gets the `count` tokens that precedes a given node or token.
   * @param node The AST node.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   */
  getTokensBefore<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node | TSESTree.Token,
    options?: number | T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
  /**
   * Gets all of the tokens between two non-overlapping nodes.
   * @param left Node before the desired token range.
   * @param right Node after the desired token range.
   * @param options The option object. If this is a number then it's `options.count`. If this is a function then it's `options.filter`.
   * @returns Tokens between left and right.
   */
  getTokensBetween<T extends SourceCode.CursorWithCountOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: number | T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
}
```
</details>

#### Methods

##### `commentsExistBetween(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token): boolean`

<details><summary>Code</summary>

```ts
commentsExistBetween(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
  ): boolean;
```
</details>

##### `getCommentsAfter(nodeOrToken: TSESTree.Node | TSESTree.Token): TSESTree.Comment[]`

<details><summary>Code</summary>

```ts
getCommentsAfter(
    nodeOrToken: TSESTree.Node | TSESTree.Token,
  ): TSESTree.Comment[];
```
</details>

##### `getCommentsBefore(nodeOrToken: TSESTree.Node | TSESTree.Token): TSESTree.Comment[]`

<details><summary>Code</summary>

```ts
getCommentsBefore(
    nodeOrToken: TSESTree.Node | TSESTree.Token,
  ): TSESTree.Comment[];
```
</details>

##### `getCommentsInside(node: TSESTree.Node): TSESTree.Comment[]`

<details><summary>Code</summary>

```ts
getCommentsInside(node: TSESTree.Node): TSESTree.Comment[];
```
</details>

##### `getFirstToken(node: TSESTree.Node, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getFirstToken<T extends SourceCode.CursorWithSkipOptions>(
    node: TSESTree.Node,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

##### `getFirstTokenBetween(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getFirstTokenBetween<T extends SourceCode.CursorWithSkipOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

##### `getFirstTokens(node: TSESTree.Node, options: T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getFirstTokens<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

##### `getFirstTokensBetween(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token, options: T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getFirstTokensBetween<T extends SourceCode.CursorWithCountOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

##### `getLastToken(node: TSESTree.Node, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getLastToken<T extends SourceCode.CursorWithSkipOptions>(
    node: TSESTree.Node,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

##### `getLastTokenBetween(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getLastTokenBetween<T extends SourceCode.CursorWithSkipOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

##### `getLastTokens(node: TSESTree.Node, options: T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getLastTokens<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

##### `getLastTokensBetween(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token, options: T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getLastTokensBetween<T extends SourceCode.CursorWithCountOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

##### `getTokenAfter(node: TSESTree.Node | TSESTree.Token, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getTokenAfter<T extends SourceCode.CursorWithSkipOptions>(
    node: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

##### `getTokenBefore(node: TSESTree.Node | TSESTree.Token, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getTokenBefore<T extends SourceCode.CursorWithSkipOptions>(
    node: TSESTree.Node | TSESTree.Token,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

##### `getTokenByRangeStart(offset: number, options: T): SourceCode.ReturnTypeFromOptions<T> | null`

<details><summary>Code</summary>

```ts
getTokenByRangeStart<T extends { includeComments?: boolean }>(
    offset: number,
    options?: T,
  ): SourceCode.ReturnTypeFromOptions<T> | null;
```
</details>

##### `getTokens(node: TSESTree.Node, beforeCount: number, afterCount: number): TSESTree.Token[]`

<details><summary>Code</summary>

```ts
getTokens(
    node: TSESTree.Node,
    beforeCount?: number,
    afterCount?: number,
  ): TSESTree.Token[];
```
</details>

##### `getTokens(node: TSESTree.Node, options: T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getTokens<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node,
    options: T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

##### `getTokensAfter(node: TSESTree.Node | TSESTree.Token, options: number | T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getTokensAfter<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node | TSESTree.Token,
    options?: number | T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

##### `getTokensBefore(node: TSESTree.Node | TSESTree.Token, options: number | T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getTokensBefore<T extends SourceCode.CursorWithCountOptions>(
    node: TSESTree.Node | TSESTree.Token,
    options?: number | T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

##### `getTokensBetween(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token, options: number | T): SourceCode.ReturnTypeFromOptions<T>[]`

<details><summary>Code</summary>

```ts
getTokensBetween<T extends SourceCode.CursorWithCountOptions>(
    left: TSESTree.Node | TSESTree.Token,
    right: TSESTree.Node | TSESTree.Token,
    options?: number | T,
  ): SourceCode.ReturnTypeFromOptions<T>[];
```
</details>

### `SourceCodeBase`

<details><summary>Class Code</summary>

```ts
declare class SourceCodeBase extends TokenStore {
  /**
   * Represents parsed source code.
   * @param ast The Program node of the AST representing the code. This AST should be created from the text that BOM was stripped.
   */
  constructor(text: string, ast: SourceCode.Program);
  /**
   * Represents parsed source code.
   * @param config The config object.
   */
  constructor(config: SourceCode.SourceCodeConfig);

  /**
   * The parsed AST for the source code.
   */
  ast: SourceCode.Program;
  applyInlineConfig(): void;
  applyLanguageOptions(): void;
  finalize(): void;
  /**
   * Retrieves an array containing all comments in the source code.
   * @returns An array of comment nodes.
   */
  getAllComments(): TSESTree.Comment[];
  /**
   * Converts a (line, column) pair into a range index.
   * @param location A line/column location
   * @returns The range index of the location in the file.
   */
  getIndexFromLoc(location: TSESTree.Position): number;
  /**
   * Gets the entire source text split into an array of lines.
   * @returns The source text as an array of lines.
   */
  getLines(): string[];
  /**
   * Converts a source text index into a (line, column) pair.
   * @param index The index of a character in a file
   * @returns A {line, column} location object with a 0-indexed column
   */
  getLocFromIndex(index: number): TSESTree.Position;
  /**
   * Gets the deepest node containing a range index.
   * @param index Range index of the desired node.
   * @returns The node if found or `null` if not found.
   */
  getNodeByRangeIndex(index: number): TSESTree.Node | null;
  /**
   * Gets the source code for the given node.
   * @param node The AST node to get the text for.
   * @param beforeCount The number of characters before the node to retrieve.
   * @param afterCount The number of characters after the node to retrieve.
   * @returns The text representing the AST node.
   */
  getText(
    node?: TSESTree.Node | TSESTree.Token,
    beforeCount?: number,
    afterCount?: number,
  ): string;
  /**
   * The flag to indicate that the source code has Unicode BOM.
   */
  hasBOM: boolean;
  /**
   * Determines if two nodes or tokens have at least one whitespace character
   * between them. Order does not matter. Returns false if the given nodes or
   * tokens overlap.
   * @param first The first node or token to check between.
   * @param second The second node or token to check between.
   * @returns True if there is a whitespace character between any of the tokens found between the two given nodes or tokens.
   */
  isSpaceBetween(
    first: TSESTree.Node | TSESTree.Token,
    second: TSESTree.Node | TSESTree.Token,
  ): boolean;
  /**
   * Determines if two nodes or tokens have at least one whitespace character
   * between them. Order does not matter. Returns false if the given nodes or
   * tokens overlap.
   * For backward compatibility, this method returns true if there are
   * `JSXText` tokens that contain whitespace between the two.
   * @param first The first node or token to check between.
   * @param second The second node or token to check between.
   * @returns {boolean} True if there is a whitespace character between
   * any of the tokens found between the two given nodes or tokens.
   * @deprecated in favor of isSpaceBetween
   */
  isSpaceBetweenTokens(first: TSESTree.Token, second: TSESTree.Token): boolean;
  /**
   * Returns the scope of the given node.
   * This information can be used track references to variables.
   */
  getScope(node: TSESTree.Node): Scope.Scope;
  /**
   * Returns an array of the ancestors of the given node, starting at
   * the root of the AST and continuing through the direct parent of the current node.
   * This array does not include the currently-traversed node itself.
   */
  getAncestors(node: TSESTree.Node): TSESTree.Node[];
  /**
   * Returns a list of variables declared by the given node.
   * This information can be used to track references to variables.
   */
  getDeclaredVariables(node: TSESTree.Node): readonly Scope.Variable[];
  /**
   * Marks a variable with the given name in the current scope as used.
   * This affects the no-unused-vars rule.
   */
  markVariableAsUsed(name: string, node: TSESTree.Node): boolean;
  /**
   * The source code split into lines according to ECMA-262 specification.
   * This is done to avoid each rule needing to do so separately.
   */
  lines: string[];
  /**
   * The indexes in `text` that each line starts
   */
  lineStartIndices: number[];
  /**
   * The parser services of this source code.
   */
  parserServices?: Partial<ParserServices>;
  /**
   * The scope of this source code.
   */
  scopeManager: Scope.ScopeManager | null;
  /**
   * The original text source code. BOM was stripped from this text.
   */
  text: string;
  /**
   * All of the tokens and comments in the AST.
   *
   * TODO: rename to 'tokens'
   */
  tokensAndComments: TSESTree.Token[];
  /**
   * The visitor keys to traverse AST.
   */
  visitorKeys: SourceCode.VisitorKeys;

  ////////////////////
  // static members //
  ////////////////////

  /**
   * Split the source code into multiple lines based on the line delimiters.
   * @param text Source code as a string.
   * @returns Array of source code lines.
   */
  static splitLines(text: string): string[];
}
```
</details>

#### Methods

##### `applyInlineConfig(): void`

<details><summary>Code</summary>

```ts
applyInlineConfig(): void;
```
</details>

##### `applyLanguageOptions(): void`

<details><summary>Code</summary>

```ts
applyLanguageOptions(): void;
```
</details>

##### `finalize(): void`

<details><summary>Code</summary>

```ts
finalize(): void;
```
</details>

##### `getAllComments(): TSESTree.Comment[]`

<details><summary>Code</summary>

```ts
getAllComments(): TSESTree.Comment[];
```
</details>

##### `getIndexFromLoc(location: TSESTree.Position): number`

<details><summary>Code</summary>

```ts
getIndexFromLoc(location: TSESTree.Position): number;
```
</details>

##### `getLines(): string[]`

<details><summary>Code</summary>

```ts
getLines(): string[];
```
</details>

##### `getLocFromIndex(index: number): TSESTree.Position`

<details><summary>Code</summary>

```ts
getLocFromIndex(index: number): TSESTree.Position;
```
</details>

##### `getNodeByRangeIndex(index: number): TSESTree.Node | null`

<details><summary>Code</summary>

```ts
getNodeByRangeIndex(index: number): TSESTree.Node | null;
```
</details>

##### `getText(node: TSESTree.Node | TSESTree.Token, beforeCount: number, afterCount: number): string`

<details><summary>Code</summary>

```ts
getText(
    node?: TSESTree.Node | TSESTree.Token,
    beforeCount?: number,
    afterCount?: number,
  ): string;
```
</details>

##### `isSpaceBetween(first: TSESTree.Node | TSESTree.Token, second: TSESTree.Node | TSESTree.Token): boolean`

<details><summary>Code</summary>

```ts
isSpaceBetween(
    first: TSESTree.Node | TSESTree.Token,
    second: TSESTree.Node | TSESTree.Token,
  ): boolean;
```
</details>

##### `isSpaceBetweenTokens(first: TSESTree.Token, second: TSESTree.Token): boolean`

<details><summary>Code</summary>

```ts
isSpaceBetweenTokens(first: TSESTree.Token, second: TSESTree.Token): boolean;
```
</details>

##### `getScope(node: TSESTree.Node): Scope.Scope`

<details><summary>Code</summary>

```ts
getScope(node: TSESTree.Node): Scope.Scope;
```
</details>

##### `getAncestors(node: TSESTree.Node): TSESTree.Node[]`

<details><summary>Code</summary>

```ts
getAncestors(node: TSESTree.Node): TSESTree.Node[];
```
</details>

##### `getDeclaredVariables(node: TSESTree.Node): readonly Scope.Variable[]`

<details><summary>Code</summary>

```ts
getDeclaredVariables(node: TSESTree.Node): readonly Scope.Variable[];
```
</details>

##### `markVariableAsUsed(name: string, node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
markVariableAsUsed(name: string, node: TSESTree.Node): boolean;
```
</details>

##### `splitLines(text: string): string[]`

<details><summary>Code</summary>

```ts
static splitLines(text: string): string[];
```
</details>

### `SourceCode`

<details><summary>Class Code</summary>

```ts
class SourceCode extends (ESLintSourceCode as typeof SourceCodeBase) {}
```
</details>


---

## Interfaces

### `Program`

<details><summary>Interface Code</summary>

```ts
export interface Program extends TSESTree.Program {
    comments: TSESTree.Comment[];
    tokens: TSESTree.Token[];
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `comments` | `TSESTree.Comment[]` | ✗ |  |
| `tokens` | `TSESTree.Token[]` | ✗ |  |

### `SourceCodeConfig`

<details><summary>Interface Code</summary>

```ts
export interface SourceCodeConfig {
    /**
     * The Program node of the AST representing the code. This AST should be created from the text that BOM was stripped.
     */
    ast: Program;
    /**
     * The parser services.
     */
    parserServices: ParserServices | null;
    /**
     * The scope of this source code.
     */
    scopeManager: Scope.ScopeManager | null;
    /**
     * The source code text.
     */
    text: string;
    /**
     * The visitor keys to traverse AST.
     */
    visitorKeys: VisitorKeys | null;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ast` | `Program` | ✗ |  |
| `parserServices` | `ParserServices | null` | ✗ |  |
| `scopeManager` | `Scope.ScopeManager | null` | ✗ |  |
| `text` | `string` | ✗ |  |
| `visitorKeys` | `VisitorKeys | null` | ✗ |  |


---

## Type Aliases

### `VisitorKeys`

```ts
type VisitorKeys = Parser.VisitorKeys;
```

### `FilterPredicate`

```ts
type FilterPredicate = (token: TSESTree.Token) => boolean;
```

### `GetFilterPredicate<Filter, Default>`

```ts
type GetFilterPredicate<Filter, Default> = Filter extends ((
      token: TSESTree.Token,
    ) => token is infer U extends TSESTree.Token)
      ? U
      : Default;
```

### `GetFilterPredicateFromOptions<Options, Default>`

```ts
type GetFilterPredicateFromOptions<Options, Default> = Options extends { filter?: FilterPredicate }
      ? GetFilterPredicate<Options['filter'], Default>
      : GetFilterPredicate<Options, Default>;
```

### `ReturnTypeFromOptions<T>`

```ts
type ReturnTypeFromOptions<T> = T extends { includeComments: true }
    ? GetFilterPredicateFromOptions<T, TSESTree.Token>
    : GetFilterPredicateFromOptions<
        T,
        Exclude<TSESTree.Token, TSESTree.Comment>
      >;
```

### `CursorWithSkipOptions`

```ts
type CursorWithSkipOptions = | number
    | FilterPredicate
    | {
        /**
         * The predicate function to choose tokens.
         */
        filter?: FilterPredicate;
        /**
         * The flag to iterate comments as well.
         */
        includeComments?: boolean;
        /**
         * The count of tokens the cursor skips.
         */
        skip?: number;
      };
```

### `CursorWithCountOptions`

```ts
type CursorWithCountOptions = | number
    | FilterPredicate
    | {
        /**
         * The maximum count of tokens the cursor iterates.
         */
        count?: number;
        /**
         * The predicate function to choose tokens.
         */
        filter?: FilterPredicate;
        /**
         * The flag to iterate comments as well.
         */
        includeComments?: boolean;
      };
```


---