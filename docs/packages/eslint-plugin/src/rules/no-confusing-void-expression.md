[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-confusing-void-expression.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 7
- **Classes**: 0
- **Imports**: 13
- **Interfaces**: 0
- **Type Aliases**: 4

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-confusing-void-expression.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `MakeRequired` | `../util` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `isClosingParenToken` | `../util` |
| `isOpeningParenToken` | `../util` |
| `isParenthesized` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |
| `getParentFunctionNode` | `../util/getParentFunctionNode` |


---

## Functions

### `wrapVoidFix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix => {
          const nodeText = context.sourceCode.getText(node);
          const newNodeText = `void ${nodeText}`;
          return fixer.replaceText(node, newNodeText);
        }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `findInvalidAncestor(node: TSESTree.Node): InvalidAncestor | null`

<details><summary>Code</summary>

```ts
function findInvalidAncestor(node: TSESTree.Node): InvalidAncestor | null {
      const parent = nullThrows(node.parent, NullThrowsReasons.MissingParent);
      if (
        parent.type === AST_NODE_TYPES.SequenceExpression &&
        node !== parent.expressions[parent.expressions.length - 1]
      ) {
        return null;
      }

      if (parent.type === AST_NODE_TYPES.ExpressionStatement) {
        // e.g. `{ console.log("foo"); }`
        // this is always valid
        return null;
      }

      if (
        parent.type === AST_NODE_TYPES.LogicalExpression &&
        parent.right === node
      ) {
        // e.g. `x && console.log(x)`
        // this is valid only if the next ancestor is valid
        return findInvalidAncestor(parent);
      }

      if (
        parent.type === AST_NODE_TYPES.ConditionalExpression &&
        (parent.consequent === node || parent.alternate === node)
      ) {
        // e.g. `cond ? console.log(true) : console.log(false)`
        // this is valid only if the next ancestor is valid
        return findInvalidAncestor(parent);
      }

      if (
        parent.type === AST_NODE_TYPES.ArrowFunctionExpression &&
        // e.g. `() => console.log("foo")`
        // this is valid with an appropriate option
        options.ignoreArrowShorthand
      ) {
        return null;
      }

      if (
        parent.type === AST_NODE_TYPES.UnaryExpression &&
        parent.operator === 'void' &&
        // e.g. `void console.log("foo")`
        // this is valid with an appropriate option
        options.ignoreVoidOperator
      ) {
        return null;
      }

      if (parent.type === AST_NODE_TYPES.ChainExpression) {
        // e.g. `console?.log('foo')`
        return findInvalidAncestor(parent);
      }

      // Any other parent is invalid.
      // We can assume a return statement will have an argument.
      return parent as InvalidAncestor;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Inspects the void expression's ancestors and finds closest invalid one.
     * By default anything other than an ExpressionStatement is invalid.
     * Parent expressions which can be used for their short-circuiting behavior
     * are ignored and their parents are checked instead.
     * @param node The void expression node to check.
     * @returns Invalid ancestor node if it was found. `null` otherwise.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `InvalidAncestor | null`
- **Calls**:
  - `nullThrows (from ../util)`
  - `findInvalidAncestor`
- **Internal Comments**:
```
// e.g. `{ console.log("foo"); }`
// this is always valid
// e.g. `x && console.log(x)`
// this is valid only if the next ancestor is valid (x2)
// e.g. `cond ? console.log(true) : console.log(false)`
// e.g. `() => console.log("foo")` (x2)
// this is valid with an appropriate option (x4)
// e.g. `void console.log("foo")` (x2)
// e.g. `console?.log('foo')`
// Any other parent is invalid.
// We can assume a return statement will have an argument.
```

### `isFinalReturn(node: TSESTree.ReturnStatement): boolean`

<details><summary>Code</summary>

```ts
function isFinalReturn(node: TSESTree.ReturnStatement): boolean {
      // the parent must be a block
      const block = nullThrows(node.parent, NullThrowsReasons.MissingParent);
      if (block.type !== AST_NODE_TYPES.BlockStatement) {
        // e.g. `if (cond) return;` (not in a block)
        return false;
      }

      // the block's parent must be a function
      const blockParent = nullThrows(
        block.parent,
        NullThrowsReasons.MissingParent,
      );
      if (
        ![
          AST_NODE_TYPES.ArrowFunctionExpression,
          AST_NODE_TYPES.FunctionDeclaration,
          AST_NODE_TYPES.FunctionExpression,
        ].includes(blockParent.type)
      ) {
        // e.g. `if (cond) { return; }`
        // not in a top-level function block
        return false;
      }

      // must be the last child of the block
      if (block.body.indexOf(node) < block.body.length - 1) {
        // not the last statement in the block
        return false;
      }

      return true;
    }
```
</details>

- **JSDoc**:
```ts
/** Checks whether the return statement is the last statement in a function body. */
```

- **Parameters**:
  - `node: TSESTree.ReturnStatement`
- **Return Type**: `boolean`
- **Calls**:
  - `nullThrows (from ../util)`
  - `[
          AST_NODE_TYPES.ArrowFunctionExpression,
          AST_NODE_TYPES.FunctionDeclaration,
          AST_NODE_TYPES.FunctionExpression,
        ].includes`
  - `block.body.indexOf`
- **Internal Comments**:
```
// the parent must be a block (x2)
// e.g. `if (cond) return;` (not in a block)
// the block's parent must be a function (x2)
// e.g. `if (cond) { return; }`
// not in a top-level function block
// must be the last child of the block
// not the last statement in the block
```

### `isPreventingASI(node: TSESTree.Expression): boolean`

<details><summary>Code</summary>

```ts
function isPreventingASI(node: TSESTree.Expression): boolean {
      const startToken = nullThrows(
        context.sourceCode.getFirstToken(node),
        NullThrowsReasons.MissingToken('first token', node.type),
      );

      return ['(', '[', '`'].includes(startToken.value);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks whether the given node, if placed on its own line,
     * would prevent automatic semicolon insertion on the line before.
     *
     * This happens if the line begins with `(`, `[` or `` ` ``
     */
```

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `boolean`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `['(', '[', '`'].includes`
### `canFix(node: ReturnStatementWithArgument | TSESTree.ArrowFunctionExpression): boolean`

<details><summary>Code</summary>

```ts
function canFix(
      node: ReturnStatementWithArgument | TSESTree.ArrowFunctionExpression,
    ): boolean {
      const targetNode =
        node.type === AST_NODE_TYPES.ReturnStatement
          ? node.argument
          : node.body;

      const type = getConstrainedTypeAtLocation(services, targetNode);
      return tsutils.isTypeFlagSet(type, ts.TypeFlags.VoidLike);
    }
```
</details>

- **Parameters**:
  - `node: ReturnStatementWithArgument | TSESTree.ArrowFunctionExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `tsutils.isTypeFlagSet`
### `isFunctionReturnTypeIncludesVoid(functionType: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isFunctionReturnTypeIncludesVoid(functionType: ts.Type): boolean {
      const callSignatures = tsutils.getCallSignaturesOfType(functionType);

      return callSignatures.some(signature => {
        const returnType = signature.getReturnType();

        return tsutils
          .unionConstituents(returnType)
          .some(tsutils.isIntrinsicVoidType);
      });
    }
```
</details>

- **Parameters**:
  - `functionType: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.getCallSignaturesOfType`
  - `callSignatures.some`
  - `signature.getReturnType`
  - `tsutils
          .unionConstituents(returnType)
          .some`
### `isVoidReturningFunctionNode(functionNode: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression): boolean`

<details><summary>Code</summary>

```ts
function isVoidReturningFunctionNode(
      functionNode:
        | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression,
    ): boolean {
      // Game plan:
      //   - If the function node has a type annotation, check if it includes `void`.
      //     - If it does then the function is safe to return `void` expressions in.
      //   - Otherwise, check if the function is a function-expression or an arrow-function.
      //   -   If it is, get its contextual type and bail if we cannot.
      //   - Return based on whether the contextual type includes `void` or not

      const functionTSNode = services.esTreeNodeToTSNodeMap.get(functionNode);

      if (functionTSNode.type) {
        const returnType = checker.getTypeFromTypeNode(functionTSNode.type);

        return tsutils
          .unionConstituents(returnType)
          .some(tsutils.isIntrinsicVoidType);
      }

      if (ts.isExpression(functionTSNode)) {
        const functionType = checker.getContextualType(functionTSNode);

        if (functionType) {
          return tsutils
            .unionConstituents(functionType)
            .some(isFunctionReturnTypeIncludesVoid);
        }
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `functionNode: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `checker.getTypeFromTypeNode`
  - `tsutils
          .unionConstituents(returnType)
          .some`
  - `ts.isExpression`
  - `checker.getContextualType`
  - `tsutils
            .unionConstituents(functionType)
            .some`
- **Internal Comments**:
```
// Game plan: (x2)
//   - If the function node has a type annotation, check if it includes `void`. (x2)
//     - If it does then the function is safe to return `void` expressions in. (x2)
//   - Otherwise, check if the function is a function-expression or an arrow-function. (x2)
//   -   If it is, get its contextual type and bail if we cannot. (x2)
//   - Return based on whether the contextual type includes `void` or not (x2)
```


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    ignoreArrowShorthand?: boolean;
    ignoreVoidOperator?: boolean;
    ignoreVoidReturningFunctions?: boolean;
  },
];
```

### `MessageId`

```ts
type MessageId = | 'invalidVoidExpr'
  | 'invalidVoidExprArrow'
  | 'invalidVoidExprArrowWrapVoid'
  | 'invalidVoidExprReturn'
  | 'invalidVoidExprReturnLast'
  | 'invalidVoidExprReturnWrapVoid'
  | 'invalidVoidExprWrapVoid'
  | 'voidExprWrapVoid';
```

### `ReturnStatementWithArgument`

```ts
type ReturnStatementWithArgument = MakeRequired<
      TSESTree.ReturnStatement,
      'argument'
    >;
```

### `InvalidAncestor`

```ts
type InvalidAncestor = | Exclude<TSESTree.Node, TSESTree.ReturnStatement>
      | ReturnStatementWithArgument;
```


---