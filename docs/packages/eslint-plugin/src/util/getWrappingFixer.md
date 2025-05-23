[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getWrappingFixer.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 7
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getWrappingFixer.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ASTUtils` | `@typescript-eslint/utils` |
| `ESLintUtils` | `@typescript-eslint/utils` |


---

## Functions

### `getWrappingFixer(params: WrappingFixerParams): (fixer: TSESLint.RuleFixer) => TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
export function getWrappingFixer(
  params: WrappingFixerParams,
): (fixer: TSESLint.RuleFixer) => TSESLint.RuleFix {
  const { node, innerNode = node, sourceCode, wrap } = params;
  const innerNodes = Array.isArray(innerNode) ? innerNode : [innerNode];

  return (fixer): TSESLint.RuleFix => {
    const innerCodes = innerNodes.map(innerNode => {
      let code = sourceCode.getText(innerNode);

      /**
       * Wrap our node in parens to prevent the following cases:
       * - It has a weaker precedence than the code we are wrapping it in
       * - It's gotten mistaken as block statement instead of object expression
       */
      if (
        !isStrongPrecedenceNode(innerNode) ||
        isObjectExpressionInOneLineReturn(node, innerNode)
      ) {
        code = `(${code})`;
      }

      return code;
    });

    if (!wrap) {
      return fixer.replaceText(node, innerCodes.join(''));
    }

    // do the wrapping
    let code = wrap(...innerCodes);

    // check the outer expression's precedence
    if (
      isWeakPrecedenceParent(node) &&
      // we wrapped the node in some expression which very likely has a different precedence than original wrapped node
      // let's wrap the whole expression in parens just in case
      !ASTUtils.isParenthesized(node, sourceCode)
    ) {
      code = `(${code})`;
    }

    // check if we need to insert semicolon
    if (/^[`([]/.test(code) && isMissingSemicolonBefore(node, sourceCode)) {
      code = `;${code}`;
    }

    return fixer.replaceText(node, code);
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Wraps node with some code. Adds parentheses as necessary.
 * @returns Fixer which adds the specified code and parens if necessary.
 */
```

- **Parameters**:
  - `params: WrappingFixerParams`
- **Return Type**: `(fixer: TSESLint.RuleFixer) => TSESLint.RuleFix`
- **Calls**:
  - `Array.isArray`
  - `innerNodes.map`
  - `sourceCode.getText`
  - `isStrongPrecedenceNode`
  - `isObjectExpressionInOneLineReturn`
  - `fixer.replaceText`
  - `innerCodes.join`
  - `wrap`
  - `isWeakPrecedenceParent`
  - `ASTUtils.isParenthesized`
  - `/^[`([]/.test`
  - `isMissingSemicolonBefore`
- **Internal Comments**:
```
/**
       * Wrap our node in parens to prevent the following cases:
       * - It has a weaker precedence than the code we are wrapping it in
       * - It's gotten mistaken as block statement instead of object expression
       */
// do the wrapping (x2)
// check the outer expression's precedence
// we wrapped the node in some expression which very likely has a different precedence than original wrapped node
// let's wrap the whole expression in parens just in case
// check if we need to insert semicolon
```

### `getMovedNodeCode(params: {
  destinationNode: TSESTree.Node;
  nodeToMove: TSESTree.Node;
  sourceCode: Readonly<TSESLint.SourceCode>;
}): string`

<details><summary>Code</summary>

```ts
export function getMovedNodeCode(params: {
  destinationNode: TSESTree.Node;
  nodeToMove: TSESTree.Node;
  sourceCode: Readonly<TSESLint.SourceCode>;
}): string {
  const { destinationNode, nodeToMove: existingNode, sourceCode } = params;
  const code = sourceCode.getText(existingNode);
  if (isStrongPrecedenceNode(existingNode)) {
    // Moved node never needs parens
    return code;
  }

  if (!isWeakPrecedenceParent(destinationNode)) {
    // Destination would never needs parens, regardless what node moves there
    return code;
  }

  // Parens may be necessary
  return `(${code})`;
}
```
</details>

- **JSDoc**:
```ts
/**
 * If the node to be moved and the destination node require parentheses, include parentheses in the node to be moved.
 * @param sourceCode Source code of current file
 * @param nodeToMove Nodes that need to be moved
 * @param destinationNode Final destination node with nodeToMove
 * @returns If parentheses are required, code for the nodeToMove node is returned with parentheses at both ends of the code.
 */
```

- **Parameters**:
  - `params: {
  destinationNode: TSESTree.Node;
  nodeToMove: TSESTree.Node;
  sourceCode: Readonly<TSESLint.SourceCode>;
}`
- **Return Type**: `string`
- **Calls**:
  - `sourceCode.getText`
  - `isStrongPrecedenceNode`
  - `isWeakPrecedenceParent`
- **Internal Comments**:
```
// Moved node never needs parens
// Destination would never needs parens, regardless what node moves there
// Parens may be necessary
```

### `isStrongPrecedenceNode(innerNode: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
export function isStrongPrecedenceNode(innerNode: TSESTree.Node): boolean {
  return (
    innerNode.type === AST_NODE_TYPES.Literal ||
    innerNode.type === AST_NODE_TYPES.Identifier ||
    innerNode.type === AST_NODE_TYPES.TSTypeReference ||
    innerNode.type === AST_NODE_TYPES.TSTypeOperator ||
    innerNode.type === AST_NODE_TYPES.ArrayExpression ||
    innerNode.type === AST_NODE_TYPES.ObjectExpression ||
    innerNode.type === AST_NODE_TYPES.MemberExpression ||
    innerNode.type === AST_NODE_TYPES.CallExpression ||
    innerNode.type === AST_NODE_TYPES.NewExpression ||
    innerNode.type === AST_NODE_TYPES.TaggedTemplateExpression ||
    innerNode.type === AST_NODE_TYPES.TSInstantiationExpression
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if a node will always have the same precedence if its parent changes.
 */
```

- **Parameters**:
  - `innerNode: TSESTree.Node`
- **Return Type**: `boolean`
### `isWeakPrecedenceParent(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isWeakPrecedenceParent(node: TSESTree.Node): boolean {
  const parent = node.parent;
  if (!parent) {
    return false;
  }

  if (
    parent.type === AST_NODE_TYPES.UpdateExpression ||
    parent.type === AST_NODE_TYPES.UnaryExpression ||
    parent.type === AST_NODE_TYPES.BinaryExpression ||
    parent.type === AST_NODE_TYPES.LogicalExpression ||
    parent.type === AST_NODE_TYPES.ConditionalExpression ||
    parent.type === AST_NODE_TYPES.AwaitExpression
  ) {
    return true;
  }

  if (
    parent.type === AST_NODE_TYPES.MemberExpression &&
    parent.object === node
  ) {
    return true;
  }

  if (
    (parent.type === AST_NODE_TYPES.CallExpression ||
      parent.type === AST_NODE_TYPES.NewExpression) &&
    parent.callee === node
  ) {
    return true;
  }

  if (
    parent.type === AST_NODE_TYPES.TaggedTemplateExpression &&
    parent.tag === node
  ) {
    return true;
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if a node's parent could have different precedence if the node changes.
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `isMissingSemicolonBefore(node: TSESTree.Node, sourceCode: TSESLint.SourceCode): boolean`

<details><summary>Code</summary>

```ts
function isMissingSemicolonBefore(
  node: TSESTree.Node,
  sourceCode: TSESLint.SourceCode,
): boolean {
  for (;;) {
    // https://github.com/typescript-eslint/typescript-eslint/issues/6225
    // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
    const parent = node.parent!;

    if (parent.type === AST_NODE_TYPES.ExpressionStatement) {
      const block = parent.parent;
      if (
        block.type === AST_NODE_TYPES.Program ||
        block.type === AST_NODE_TYPES.BlockStatement
      ) {
        // parent is an expression statement in a block
        const statementIndex = block.body.indexOf(parent);
        const previousStatement = block.body[statementIndex - 1];
        if (
          statementIndex > 0 &&
          ESLintUtils.nullThrows(
            sourceCode.getLastToken(previousStatement),
            'Mismatched semicolon and block',
          ).value !== ';'
        ) {
          return true;
        }
      }
    }

    if (!isLeftHandSide(node)) {
      return false;
    }

    node = parent;
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if a node is at the beginning of expression statement and the statement above doesn't end with semicolon.
 * Doesn't check if the node begins with `(`, `[` or `` ` ``.
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `sourceCode: TSESLint.SourceCode`
- **Return Type**: `boolean`
- **Calls**:
  - `block.body.indexOf`
  - `ESLintUtils.nullThrows`
  - `sourceCode.getLastToken`
  - `isLeftHandSide`
- **Internal Comments**:
```
// https://github.com/typescript-eslint/typescript-eslint/issues/6225 (x2)
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
// parent is an expression statement in a block (x2)
```

### `isLeftHandSide(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isLeftHandSide(node: TSESTree.Node): boolean {
  // https://github.com/typescript-eslint/typescript-eslint/issues/6225
  // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
  const parent = node.parent!;

  // a++
  if (parent.type === AST_NODE_TYPES.UpdateExpression) {
    return true;
  }

  // a + b
  if (
    (parent.type === AST_NODE_TYPES.BinaryExpression ||
      parent.type === AST_NODE_TYPES.LogicalExpression ||
      parent.type === AST_NODE_TYPES.AssignmentExpression) &&
    node === parent.left
  ) {
    return true;
  }

  // a ? b : c
  if (
    parent.type === AST_NODE_TYPES.ConditionalExpression &&
    node === parent.test
  ) {
    return true;
  }

  // a(b)
  if (parent.type === AST_NODE_TYPES.CallExpression && node === parent.callee) {
    return true;
  }

  // a`b`
  if (
    parent.type === AST_NODE_TYPES.TaggedTemplateExpression &&
    node === parent.tag
  ) {
    return true;
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a node is LHS of an operator.
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Internal Comments**:
```
// https://github.com/typescript-eslint/typescript-eslint/issues/6225 (x2)
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
// a++
// a + b
// a ? b : c
// a(b)
// a`b`
```

### `isObjectExpressionInOneLineReturn(node: TSESTree.Node, innerNode: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isObjectExpressionInOneLineReturn(
  node: TSESTree.Node,
  innerNode: TSESTree.Node,
): boolean {
  return (
    node.parent?.type === AST_NODE_TYPES.ArrowFunctionExpression &&
    node.parent.body === node &&
    innerNode.type === AST_NODE_TYPES.ObjectExpression
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a node's parent is arrow function expression and a inner node is object expression
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `innerNode: TSESTree.Node`
- **Return Type**: `boolean`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `WrappingFixerParams`

<details><summary>Interface Code</summary>

```ts
interface WrappingFixerParams {
  /**
   * Descendant of `node` we want to preserve.
   * Use this to replace some code with another.
   * By default it's the node we are modifying (so nothing is removed).
   * You can pass multiple nodes as an array.
   */
  innerNode?: TSESTree.Node | TSESTree.Node[];
  /** The node we want to modify. */
  node: TSESTree.Node;
  /** Source code. */
  sourceCode: Readonly<TSESLint.SourceCode>;
  /**
   * The function which gets the code of the `innerNode` and returns some code around it.
   * Receives multiple arguments if there are multiple innerNodes.
   * E.g. ``code => `${code} != null` ``
   */
  wrap?: (...code: string[]) => string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `innerNode` | `TSESTree.Node | TSESTree.Node[]` | ✓ |  |
| `node` | `TSESTree.Node` | ✗ |  |
| `sourceCode` | `Readonly<TSESLint.SourceCode>` | ✗ |  |
| `wrap` | `(...code: string[]) => string` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---