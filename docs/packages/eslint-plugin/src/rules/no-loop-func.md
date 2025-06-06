[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-loop-func.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 14 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-loop-func.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `SKIPPED_IIFE_NODES` | `Set<any>` | const | `new Set<
      | TSESTree.ArrowFunctionExpression
      | TSESTree.FunctionDeclaration
      | TSESTree.FunctionExpression
    >()` | ✗ |
| `parent` | `any` | const | `currentNode.parent` | ✗ |
| `border` | `any` | const | `excludedNode ? excludedNode.range[1] : 0` | ✗ |
| `retv` | `TSESTree.Node` | let/var | `node` | ✗ |
| `containingLoopNode` | `TSESTree.Node | null` | let/var | `node` | ✗ |
| `variable` | `any` | const | `reference.resolved` | ✗ |
| `definition` | `any` | const | `variable?.defs[0]` | ✗ |
| `declaration` | `any` | const | `definition?.parent` | ✗ |
| `kind` | `any` | const | `declaration?.type === AST_NODE_TYPES.VariableDeclaration
          ? declaration.kind
          : ''` | ✗ |
| `border` | `any` | const | `getTopLoopNode(
        loopNode,
        kind === 'let' ? declaration : null,
      ).range[0]` | ✗ |
| `id` | `any` | const | `upperRef.identifier` | ✗ |
| `references` | `any` | const | `context.sourceCode.getScope(node).through` | ✗ |
| `isFunctionExpression` | `boolean` | const | `node.type === AST_NODE_TYPES.FunctionExpression` | ✗ |
| `isFunctionReferenced` | `any` | const | `isFunctionExpression && node.id
            ? references.some(r => r.identifier.name === node.id?.name)
            : false` | ✗ |


---

## Functions

### `getContainingLoopNode(node: TSESTree.Node): TSESTree.Node | null`

<details><summary>Code</summary>

```ts
function getContainingLoopNode(node: TSESTree.Node): TSESTree.Node | null {
      for (
        let currentNode = node;
        currentNode.parent;
        currentNode = currentNode.parent
      ) {
        const parent = currentNode.parent;

        switch (parent.type) {
          case AST_NODE_TYPES.WhileStatement:
          case AST_NODE_TYPES.DoWhileStatement:
            return parent;

          case AST_NODE_TYPES.ForStatement:
            // `init` is outside of the loop.
            if (parent.init !== currentNode) {
              return parent;
            }
            break;

          case AST_NODE_TYPES.ForInStatement:
          case AST_NODE_TYPES.ForOfStatement:
            // `right` is outside of the loop.
            if (parent.right !== currentNode) {
              return parent;
            }
            break;

          case AST_NODE_TYPES.ArrowFunctionExpression:
          case AST_NODE_TYPES.FunctionExpression:
          case AST_NODE_TYPES.FunctionDeclaration:
            // We don't need to check nested functions.

            // We need to check nested functions only in case of IIFE.
            if (SKIPPED_IIFE_NODES.has(parent)) {
              break;
            }
            return null;

          default:
            break;
        }
      }

      return null;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Gets the containing loop node of a specified node.
     *
     * We don't need to check nested functions, so this ignores those.
     * `Scope.through` contains references of nested functions.
     *
     * @param node An AST node to get.
     * @returns The containing loop node of the specified node, or `null`.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `TSESTree.Node | null`
- **Calls**:
  - `SKIPPED_IIFE_NODES.has`
- **Internal Comments**:
```
// `init` is outside of the loop.
// `right` is outside of the loop.
// We don't need to check nested functions.
// We need to check nested functions only in case of IIFE.
```

### `getTopLoopNode(node: TSESTree.Node, excludedNode: TSESTree.Node | null | undefined): TSESTree.Node`

<details><summary>Code</summary>

```ts
function getTopLoopNode(
      node: TSESTree.Node,
      excludedNode: TSESTree.Node | null | undefined,
    ): TSESTree.Node {
      const border = excludedNode ? excludedNode.range[1] : 0;
      let retv = node;
      let containingLoopNode: TSESTree.Node | null = node;

      while (containingLoopNode && containingLoopNode.range[0] >= border) {
        retv = containingLoopNode;
        containingLoopNode = getContainingLoopNode(containingLoopNode);
      }

      return retv;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Gets the containing loop node of a given node.
     * If the loop was nested, this returns the most outer loop.
     * @param node A node to get. This is a loop node.
     * @param excludedNode A node that the result node should not include.
     * @returns The most outer loop node.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `excludedNode: TSESTree.Node | null | undefined`
- **Return Type**: `TSESTree.Node`
- **Calls**:
  - `getContainingLoopNode`
### `isSafe(loopNode: TSESTree.Node, reference: TSESLint.Scope.Reference): boolean`

<details><summary>Code</summary>

```ts
function isSafe(
      loopNode: TSESTree.Node,
      reference: TSESLint.Scope.Reference,
    ): boolean {
      const variable = reference.resolved;
      const definition = variable?.defs[0];
      const declaration = definition?.parent;
      const kind =
        declaration?.type === AST_NODE_TYPES.VariableDeclaration
          ? declaration.kind
          : '';

      // type references are all safe
      // this only really matters for global types that haven't been configured
      if (reference.isTypeReference) {
        return true;
      }

      // Variables which are declared by `const` is safe.
      if (kind === 'const') {
        return true;
      }

      /*
       * Variables which are declared by `let` in the loop is safe.
       * It's a different instance from the next loop step's.
       */
      if (
        kind === 'let' &&
        declaration &&
        declaration.range[0] > loopNode.range[0] &&
        declaration.range[1] < loopNode.range[1]
      ) {
        return true;
      }

      /*
       * WriteReferences which exist after this border are unsafe because those
       * can modify the variable.
       */
      const border = getTopLoopNode(
        loopNode,
        kind === 'let' ? declaration : null,
      ).range[0];

      /**
       * Checks whether a given reference is safe or not.
       * The reference is every reference of the upper scope's variable we are
       * looking now.
       *
       * It's safe if the reference matches one of the following condition.
       * - is readonly.
       * - doesn't exist inside a local function and after the border.
       *
       * @param upperRef A reference to check.
       * @returns `true` if the reference is safe.
       */
      function isSafeReference(upperRef: TSESLint.Scope.Reference): boolean {
        const id = upperRef.identifier;

        return (
          !upperRef.isWrite() ||
          (variable?.scope.variableScope === upperRef.from.variableScope &&
            id.range[0] < border)
        );
      }

      return variable?.references.every(isSafeReference) ?? false;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks whether a given reference which refers to an upper scope's variable is
     * safe or not.
     * @param loopNode A containing loop node.
     * @param reference A reference to check.
     * @returns `true` if the reference is safe or not.
     */
```

- **Parameters**:
  - `loopNode: TSESTree.Node`
  - `reference: TSESLint.Scope.Reference`
- **Return Type**: `boolean`
- **Calls**:
  - `getTopLoopNode`
  - `upperRef.isWrite`
  - `variable?.references.every`
- **Internal Comments**:
```
// type references are all safe
// this only really matters for global types that haven't been configured
// Variables which are declared by `const` is safe.
/*
       * Variables which are declared by `let` in the loop is safe.
       * It's a different instance from the next loop step's.
       */
/*
       * WriteReferences which exist after this border are unsafe because those
       * can modify the variable.
       */ (x2)
/**
       * Checks whether a given reference is safe or not.
       * The reference is every reference of the upper scope's variable we are
       * looking now.
       *
       * It's safe if the reference matches one of the following condition.
       * - is readonly.
       * - doesn't exist inside a local function and after the border.
       *
       * @param upperRef A reference to check.
       * @returns `true` if the reference is safe.
       */
```

### `isSafeReference(upperRef: TSESLint.Scope.Reference): boolean`

<details><summary>Code</summary>

```ts
function isSafeReference(upperRef: TSESLint.Scope.Reference): boolean {
        const id = upperRef.identifier;

        return (
          !upperRef.isWrite() ||
          (variable?.scope.variableScope === upperRef.from.variableScope &&
            id.range[0] < border)
        );
      }
```
</details>

- **JSDoc**:
```ts
/**
       * Checks whether a given reference is safe or not.
       * The reference is every reference of the upper scope's variable we are
       * looking now.
       *
       * It's safe if the reference matches one of the following condition.
       * - is readonly.
       * - doesn't exist inside a local function and after the border.
       *
       * @param upperRef A reference to check.
       * @returns `true` if the reference is safe.
       */
```

- **Parameters**:
  - `upperRef: TSESLint.Scope.Reference`
- **Return Type**: `boolean`
- **Calls**:
  - `upperRef.isWrite`
### `checkForLoops(node: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression): void`

<details><summary>Code</summary>

```ts
function checkForLoops(
      node:
        | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression,
    ): void {
      const loopNode = getContainingLoopNode(node);

      if (!loopNode) {
        return;
      }

      const references = context.sourceCode.getScope(node).through;

      if (!(node.async || node.generator) && isIIFE(node)) {
        const isFunctionExpression =
          node.type === AST_NODE_TYPES.FunctionExpression;

        // Check if the function is referenced elsewhere in the code
        const isFunctionReferenced =
          isFunctionExpression && node.id
            ? references.some(r => r.identifier.name === node.id?.name)
            : false;

        if (!isFunctionReferenced) {
          SKIPPED_IIFE_NODES.add(node);
          return;
        }
      }

      const unsafeRefs = references
        .filter(r => r.resolved && !isSafe(loopNode, r))
        .map(r => r.identifier.name);

      if (unsafeRefs.length > 0) {
        context.report({
          node,
          messageId: 'unsafeRefs',
          data: { varNames: `'${unsafeRefs.join("', '")}'` },
        });
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Reports functions which match the following condition:
     * - has a loop node in ancestors.
     * - has any references which refers to an unsafe variable.
     *
     * @param node The AST node to check.
     */
```

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression`
- **Return Type**: `void`
- **Calls**:
  - `getContainingLoopNode`
  - `context.sourceCode.getScope`
  - `isIIFE`
  - `references.some`
  - `SKIPPED_IIFE_NODES.add`
  - `references
        .filter(r => r.resolved && !isSafe(loopNode, r))
        .map`
  - `context.report`
  - `unsafeRefs.join`
- **Internal Comments**:
```
// Check if the function is referenced elsewhere in the code (x2)
```

### `isIIFE(node: | TSESTree.ArrowFunctionExpression
    | TSESTree.FunctionDeclaration
    | TSESTree.FunctionExpression): boolean`

<details><summary>Code</summary>

```ts
function isIIFE(
  node:
    | TSESTree.ArrowFunctionExpression
    | TSESTree.FunctionDeclaration
    | TSESTree.FunctionExpression,
): boolean {
  return (
    node.parent.type === AST_NODE_TYPES.CallExpression &&
    node.parent.callee === node
  );
}
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
    | TSESTree.FunctionDeclaration
    | TSESTree.FunctionExpression`
- **Return Type**: `boolean`

---

## Type Aliases

### `Options`

```ts
type Options = InferOptionsTypeFromRule<typeof baseRule>;
```

### `MessageIds`

```ts
type MessageIds = InferMessageIdsTypeFromRule<typeof baseRule>;
```


---