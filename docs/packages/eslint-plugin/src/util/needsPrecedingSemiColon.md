[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `needsPrecedingSemiColon.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 8 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `BREAK_OR_CONTINUE` | `Set<any>` | const | `new Set([
  AST_NODE_TYPES.BreakStatement,
  AST_NODE_TYPES.ContinueStatement,
])` | ✗ |
| `DECLARATIONS` | `Set<any>` | const | `new Set([
  AST_NODE_TYPES.ExportAllDeclaration,
  AST_NODE_TYPES.ExportNamedDeclaration,
  AST_NODE_TYPES.ImportDeclaration,
])` | ✗ |
| `IDENTIFIER_OR_KEYWORD` | `Set<any>` | const | `new Set([
  AST_NODE_TYPES.Identifier,
  AST_TOKEN_TYPES.Keyword,
])` | ✗ |
| `NODE_TYPES_BY_KEYWORD` | `Record<string, TSESTree.AST_NODE_TYPES | null>` | const | `{
  __proto__: null,
  break: AST_NODE_TYPES.BreakStatement,
  continue: AST_NODE_TYPES.ContinueStatement,
  debugger: AST_NODE_TYPES.DebuggerStatement,
  do: AST_NODE_TYPES.DoWhileStatement,
  else: AST_NODE_TYPES.IfStatement,
  return: AST_NODE_TYPES.ReturnStatement,
  yield: AST_NODE_TYPES.YieldExpression,
}` | ✗ |
| `PUNCTUATORS` | `Set<string>` | const | `new Set(['--', ';', ':', '{', '++', '=>'])` | ✗ |
| `STATEMENTS` | `Set<any>` | const | `new Set([
  AST_NODE_TYPES.DoWhileStatement,
  AST_NODE_TYPES.ForInStatement,
  AST_NODE_TYPES.ForOfStatement,
  AST_NODE_TYPES.ForStatement,
  AST_NODE_TYPES.IfStatement,
  AST_NODE_TYPES.WhileStatement,
  AST_NODE_TYPES.WithStatement,
])` | ✗ |
| `keyword` | `any` | const | `prevToken.value` | ✗ |
| `nodeType` | `any` | const | `NODE_TYPES_BY_KEYWORD[keyword]` | ✗ |


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