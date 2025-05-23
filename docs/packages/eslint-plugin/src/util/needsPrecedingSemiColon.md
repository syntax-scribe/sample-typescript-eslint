[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `needsPrecedingSemiColon.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/needsPrecedingSemiColon.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `SourceCode` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `isClosingBraceToken` | `@typescript-eslint/utils/ast-utils` |
| `isClosingParenToken` | `@typescript-eslint/utils/ast-utils` |


---

## Functions

### `needsPrecedingSemicolon(sourceCode: SourceCode, node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
export function needsPrecedingSemicolon(
  sourceCode: SourceCode,
  node: TSESTree.Node,
): boolean {
  const prevToken = sourceCode.getTokenBefore(node);

  if (
    !prevToken ||
    (prevToken.type === AST_TOKEN_TYPES.Punctuator &&
      PUNCTUATORS.has(prevToken.value))
  ) {
    return false;
  }

  const prevNode = sourceCode.getNodeByRangeIndex(prevToken.range[0]);

  if (!prevNode) {
    return false;
  }

  if (isClosingParenToken(prevToken)) {
    return !STATEMENTS.has(prevNode.type);
  }

  if (isClosingBraceToken(prevToken)) {
    return (
      (prevNode.type === AST_NODE_TYPES.BlockStatement &&
        prevNode.parent.type === AST_NODE_TYPES.FunctionExpression &&
        prevNode.parent.parent.type !== AST_NODE_TYPES.MethodDefinition) ||
      (prevNode.type === AST_NODE_TYPES.ClassBody &&
        prevNode.parent.type === AST_NODE_TYPES.ClassExpression) ||
      prevNode.type === AST_NODE_TYPES.ObjectExpression
    );
  }

  if (!prevNode.parent) {
    return false;
  }

  if (IDENTIFIER_OR_KEYWORD.has(prevToken.type)) {
    if (BREAK_OR_CONTINUE.has(prevNode.parent.type)) {
      return false;
    }

    const keyword = prevToken.value;
    const nodeType = NODE_TYPES_BY_KEYWORD[keyword];

    return prevNode.type !== nodeType;
  }

  if (prevToken.type === AST_TOKEN_TYPES.String) {
    return !DECLARATIONS.has(prevNode.parent.type);
  }

  return true;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Determines whether an opening parenthesis `(`, bracket `[` or backtick ``` ` ``` needs to be preceded by a semicolon.
 * This opening parenthesis or bracket should be at the start of an `ExpressionStatement`, a `MethodDefinition` or at
 * the start of the body of an `ArrowFunctionExpression`.
 * @param sourceCode The source code object.
 * @param node A node at the position where an opening parenthesis or bracket will be inserted.
 * @returns Whether a semicolon is required before the opening parenthesis or bracket.
 */
```

- **Parameters**:
  - `sourceCode: SourceCode`
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `sourceCode.getTokenBefore`
  - `PUNCTUATORS.has`
  - `sourceCode.getNodeByRangeIndex`
  - `isClosingParenToken (from @typescript-eslint/utils/ast-utils)`
  - `STATEMENTS.has`
  - `isClosingBraceToken (from @typescript-eslint/utils/ast-utils)`
  - `IDENTIFIER_OR_KEYWORD.has`
  - `BREAK_OR_CONTINUE.has`
  - `DECLARATIONS.has`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---