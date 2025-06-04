[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `return-await.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 46 |
| 📦 Imports | 12 |
| 📊 Variables & Constants | 15 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/return-await.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `Awaitable` | `../util` |
| `createRule` | `../util` |
| `getFixOrSuggest` | `../util` |
| `getParserServices` | `../util` |
| `isAwaitExpression` | `../util` |
| `isAwaitKeyword` | `../util` |
| `needsToBeAwaited` | `../util` |
| `nullThrows` | `../util` |
| `isHigherPrecedenceThanAwait` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `scopeInfoStack` | `ScopeInfo[]` | const | `[]` | ✗ |
| `functionScope` | `any` | const | `scope.variableScope` | ✗ |
| `declaration` | `any` | const | `variable.defs[0]` | ✗ |
| `declaratorNode` | `any` | const | `declaration.node` | ✗ |
| `declarationNode` | `TSESTree.VariableDeclaration` | const | `declaratorNode.parent as TSESTree.VariableDeclaration` | ✗ |
| `__never` | `never` | const | `block` | ✗ |
| `child` | `ts.Node` | let/var | `node` | ✗ |
| `ancestor` | `any` | let/var | `node.parent as ts.Node | undefined` | ✗ |
| `block` | `'catch' | 'finally' | 'try' | undefined` | let/var | `*not shown*` | ✗ |
| `startAt` | `any` | const | `awaitToken.range[0]` | ✗ |
| `endAt` | `any` | let/var | `awaitToken.range[1]` | ✗ |
| `child` | `ts.Node` | let/var | `*not shown*` | ✗ |
| `affectsErrorHandling` | `boolean` | const | `affectsExplicitErrorHandling(expression) ||
        affectsExplicitResourceManagement(node)` | ✗ |
| `useAutoFix` | `boolean` | const | `!affectsErrorHandling` | ✗ |
| `shouldAwaitInCurrentContext` | `WhetherToAwait` | const | `affectsErrorHandling
        ? ruleConfiguration.errorHandlingContext
        : ruleConfiguration.ordinaryContext` | ✗ |


---

## Functions

### `enterFunction(node: FunctionNode): void`

<details><summary>Code</summary>

```ts
function enterFunction(node: FunctionNode): void {
      scopeInfoStack.push({
        hasAsync: node.async,
        owningFunc: node,
      });
    }
```
</details>

- **Parameters**:
  - `node: FunctionNode`
- **Return Type**: `void`
- **Calls**:
  - `scopeInfoStack.push`
### `exitFunction(): void`

<details><summary>Code</summary>

```ts
function exitFunction(): void {
      scopeInfoStack.pop();
    }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `scopeInfoStack.pop`
### `affectsExplicitResourceManagement(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function affectsExplicitResourceManagement(node: TSESTree.Node): boolean {
      // just need to determine if there is a `using` declaration in scope.
      let scope = context.sourceCode.getScope(node);
      const functionScope = scope.variableScope;
      while (true) {
        for (const variable of scope.variables) {
          if (variable.defs.length !== 1) {
            // This can't be the case for `using` or `await using` since it's
            // an error to redeclare those more than once in the same scope,
            // unlike, say, `var` declarations.
            continue;
          }

          const declaration = variable.defs[0];
          const declaratorNode = declaration.node;
          const declarationNode =
            declaratorNode.parent as TSESTree.VariableDeclaration;

          // if it's a using/await using declaration, and it comes _before_ the
          // node we're checking, it affects control flow for that node.
          if (
            ['await using', 'using'].includes(declarationNode.kind) &&
            declaratorNode.range[1] < node.range[0]
          ) {
            return true;
          }
        }

        if (scope === functionScope) {
          // We've checked all the relevant scopes
          break;
        }

        // This should always exist, since the rule should only be checking
        // contexts in which `return` statements are legal, which should always
        // be inside a function.
        scope = nullThrows(
          scope.upper,
          'Expected parent scope to exist. return-await should only operate on return statements within functions',
        );
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode.getScope`
  - `['await using', 'using'].includes`
  - `nullThrows (from ../util)`
- **Internal Comments**:
```
// just need to determine if there is a `using` declaration in scope. (x2)
// This can't be the case for `using` or `await using` since it's
// an error to redeclare those more than once in the same scope,
// unlike, say, `var` declarations.
// if it's a using/await using declaration, and it comes _before_ the
// node we're checking, it affects control flow for that node.
// We've checked all the relevant scopes
// This should always exist, since the rule should only be checking (x3)
// contexts in which `return` statements are legal, which should always (x3)
// be inside a function. (x3)
```

### `affectsExplicitErrorHandling(node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
function affectsExplicitErrorHandling(node: ts.Node): boolean {
      // If an error-handling block is followed by another error-handling block,
      // control flow is affected by whether promises in it are awaited or not.
      // Otherwise, we need to check recursively for nested try statements until
      // we get to the top level of a function or the program. If by then,
      // there's no offending error-handling blocks, it doesn't affect control
      // flow.
      const tryAncestorResult = findContainingTryStatement(node);
      if (tryAncestorResult == null) {
        return false;
      }

      const { block, tryStatement } = tryAncestorResult;

      switch (block) {
        case 'catch':
          // Exceptions thrown in catch blocks followed by a finally block affect
          // control flow.
          if (tryStatement.finallyBlock != null) {
            return true;
          }

          // Otherwise recurse.
          return affectsExplicitErrorHandling(tryStatement);
        case 'finally':
          return affectsExplicitErrorHandling(tryStatement);
        case 'try':
          // Try blocks are always followed by either a catch or finally,
          // so exceptions thrown here always affect control flow.
          return true;
        default: {
          const __never: never = block;
          throw new Error(`Unexpected block type: ${String(__never)}`);
        }
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Tests whether a node is inside of an explicit error handling context
     * (try/catch/finally) in a way that throwing an exception will have an
     * impact on the program's control flow.
     */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `findContainingTryStatement`
  - `affectsExplicitErrorHandling`
  - `String`
- **Internal Comments**:
```
// If an error-handling block is followed by another error-handling block, (x2)
// control flow is affected by whether promises in it are awaited or not. (x2)
// Otherwise, we need to check recursively for nested try statements until (x2)
// we get to the top level of a function or the program. If by then, (x2)
// there's no offending error-handling blocks, it doesn't affect control (x2)
// flow. (x2)
// Exceptions thrown in catch blocks followed by a finally block affect
// control flow.
// Otherwise recurse.
// Try blocks are always followed by either a catch or finally,
// so exceptions thrown here always affect control flow.
```

### `findContainingTryStatement(node: ts.Node): FindContainingTryStatementResult | undefined`

<details><summary>Code</summary>

```ts
function findContainingTryStatement(
      node: ts.Node,
    ): FindContainingTryStatementResult | undefined {
      let child = node;
      let ancestor = node.parent as ts.Node | undefined;

      while (ancestor && !ts.isFunctionLike(ancestor)) {
        if (ts.isTryStatement(ancestor)) {
          let block: 'catch' | 'finally' | 'try' | undefined;
          if (child === ancestor.tryBlock) {
            block = 'try';
          } else if (child === ancestor.catchClause) {
            block = 'catch';
          } else if (child === ancestor.finallyBlock) {
            block = 'finally';
          }

          return {
            block: nullThrows(
              block,
              'Child of a try statement must be a try block, catch clause, or finally block',
            ),
            tryStatement: ancestor,
          };
        }
        child = ancestor;
        ancestor = ancestor.parent;
      }

      return undefined;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * A try _statement_ is the whole thing that encompasses try block,
     * catch clause, and finally block. This function finds the nearest
     * enclosing try statement (if present) for a given node, and reports which
     * part of the try statement the node is in.
     */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `FindContainingTryStatementResult | undefined`
- **Calls**:
  - `ts.isFunctionLike`
  - `ts.isTryStatement`
  - `nullThrows (from ../util)`
### `removeAwait(fixer: TSESLint.RuleFixer, node: TSESTree.Expression): TSESLint.RuleFix | null`

<details><summary>Code</summary>

```ts
function removeAwait(
      fixer: TSESLint.RuleFixer,
      node: TSESTree.Expression,
    ): TSESLint.RuleFix | null {
      // Should always be an await node; but let's be safe.
      /* istanbul ignore if */ if (!isAwaitExpression(node)) {
        return null;
      }

      const awaitToken = context.sourceCode.getFirstToken(node, isAwaitKeyword);
      // Should always be the case; but let's be safe.
      /* istanbul ignore if */ if (!awaitToken) {
        return null;
      }

      const startAt = awaitToken.range[0];
      let endAt = awaitToken.range[1];
      // Also remove any extraneous whitespace after `await`, if there is any.
      const nextToken = context.sourceCode.getTokenAfter(awaitToken, {
        includeComments: true,
      });
      if (nextToken) {
        endAt = nextToken.range[0];
      }

      return fixer.removeRange([startAt, endAt]);
    }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `node: TSESTree.Expression`
- **Return Type**: `TSESLint.RuleFix | null`
- **Calls**:
  - `isAwaitExpression (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `context.sourceCode.getTokenAfter`
  - `fixer.removeRange`
- **Internal Comments**:
```
// Should always be an await node; but let's be safe.
/* istanbul ignore if */ (x2)
// Should always be the case; but let's be safe.
// Also remove any extraneous whitespace after `await`, if there is any. (x2)
```

### `insertAwait(fixer: TSESLint.RuleFixer, node: TSESTree.Expression, isHighPrecendence: boolean): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
function insertAwait(
      fixer: TSESLint.RuleFixer,
      node: TSESTree.Expression,
      isHighPrecendence: boolean,
    ): TSESLint.RuleFix | TSESLint.RuleFix[] {
      if (isHighPrecendence) {
        return fixer.insertTextBefore(node, 'await ');
      }
      return [
        fixer.insertTextBefore(node, 'await ('),
        fixer.insertTextAfter(node, ')'),
      ];
    }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `node: TSESTree.Expression`
  - `isHighPrecendence: boolean`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
### `test(node: TSESTree.Expression, expression: ts.Node): void`

<details><summary>Code</summary>

```ts
function test(node: TSESTree.Expression, expression: ts.Node): void {
      let child: ts.Node;

      const isAwait = ts.isAwaitExpression(expression);

      if (isAwait) {
        child = expression.getChildAt(1);
      } else {
        child = expression;
      }

      const type = checker.getTypeAtLocation(child);
      const certainty = needsToBeAwaited(checker, expression, type);

      // handle awaited _non_thenables

      if (certainty !== Awaitable.Always) {
        if (isAwait) {
          if (certainty === Awaitable.May) {
            return;
          }
          context.report({
            node,
            messageId: 'nonPromiseAwait',
            fix: fixer => removeAwait(fixer, node),
          });
        }
        return;
      }

      // At this point it's definitely a thenable.

      const affectsErrorHandling =
        affectsExplicitErrorHandling(expression) ||
        affectsExplicitResourceManagement(node);
      const useAutoFix = !affectsErrorHandling;

      const ruleConfiguration = getConfiguration(option as Option);

      const shouldAwaitInCurrentContext = affectsErrorHandling
        ? ruleConfiguration.errorHandlingContext
        : ruleConfiguration.ordinaryContext;

      switch (shouldAwaitInCurrentContext) {
        case 'await':
          if (!isAwait) {
            context.report({
              node,
              messageId: 'requiredPromiseAwait',
              ...getFixOrSuggest({
                fixOrSuggest: useAutoFix ? 'fix' : 'suggest',
                suggestion: {
                  messageId: 'requiredPromiseAwaitSuggestion',
                  fix: fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    ),
                },
              }),
            });
          }
          break;
        case "don't-care":
          break;
        case 'no-await':
          if (isAwait) {
            context.report({
              node,
              messageId: 'disallowedPromiseAwait',
              ...getFixOrSuggest({
                fixOrSuggest: useAutoFix ? 'fix' : 'suggest',
                suggestion: {
                  messageId: 'disallowedPromiseAwaitSuggestion',
                  fix: fixer => removeAwait(fixer, node),
                },
              }),
            });
          }
          break;
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
  - `expression: ts.Node`
- **Return Type**: `void`
- **Calls**:
  - `ts.isAwaitExpression`
  - `expression.getChildAt`
  - `checker.getTypeAtLocation`
  - `needsToBeAwaited (from ../util)`
  - `context.report`
  - `removeAwait`
  - `affectsExplicitErrorHandling`
  - `affectsExplicitResourceManagement`
  - `getConfiguration`
  - `getFixOrSuggest (from ../util)`
  - `insertAwait`
  - `isHigherPrecedenceThanAwait (from ../util)`
- **Internal Comments**:
```
// handle awaited _non_thenables
// At this point it's definitely a thenable. (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `findPossiblyReturnedNodes(node: TSESTree.Expression): TSESTree.Expression[]`

<details><summary>Code</summary>

```ts
function findPossiblyReturnedNodes(
      node: TSESTree.Expression,
    ): TSESTree.Expression[] {
      if (node.type === AST_NODE_TYPES.ConditionalExpression) {
        return [
          ...findPossiblyReturnedNodes(node.alternate),
          ...findPossiblyReturnedNodes(node.consequent),
        ];
      }
      return [node];
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `TSESTree.Expression[]`
- **Calls**:
  - `findPossiblyReturnedNodes`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
                    insertAwait(
                      fixer,
                      node,
                      isHigherPrecedenceThanAwait(expression),
                    )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `insertAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => removeAwait(fixer, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `removeAwait`
### `getConfiguration(option: Option): RuleConfiguration`

<details><summary>Code</summary>

```ts
function getConfiguration(option: Option): RuleConfiguration {
  switch (option) {
    case 'always':
      return {
        errorHandlingContext: 'await',
        ordinaryContext: 'await',
      };
    case 'error-handling-correctness-only':
      return {
        errorHandlingContext: 'await',
        ordinaryContext: "don't-care",
      };
    case 'in-try-catch':
      return {
        errorHandlingContext: 'await',
        ordinaryContext: 'no-await',
      };
    case 'never':
      return {
        errorHandlingContext: 'no-await',
        ordinaryContext: 'no-await',
      };
  }
}
```
</details>

- **Parameters**:
  - `option: Option`
- **Return Type**: `RuleConfiguration`

---

## Interfaces

### `ScopeInfo`

<details><summary>Interface Code</summary>

```ts
interface ScopeInfo {
  hasAsync: boolean;
  owningFunc: FunctionNode;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `hasAsync` | `boolean` | ✗ |  |
| `owningFunc` | `FunctionNode` | ✗ |  |

### `FindContainingTryStatementResult`

<details><summary>Interface Code</summary>

```ts
interface FindContainingTryStatementResult {
      block: 'catch' | 'finally' | 'try';
      tryStatement: ts.TryStatement;
    }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `block` | `'catch' | 'finally' | 'try'` | ✗ |  |
| `tryStatement` | `ts.TryStatement` | ✗ |  |

### `RuleConfiguration`

<details><summary>Interface Code</summary>

```ts
interface RuleConfiguration {
  errorHandlingContext: WhetherToAwait;
  ordinaryContext: WhetherToAwait;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `errorHandlingContext` | `WhetherToAwait` | ✗ |  |
| `ordinaryContext` | `WhetherToAwait` | ✗ |  |


---

## Type Aliases

### `FunctionNode`

```ts
type FunctionNode = | TSESTree.ArrowFunctionExpression
  | TSESTree.FunctionDeclaration
  | TSESTree.FunctionExpression;
```

### `Option`

```ts
type Option = | 'always'
  | 'error-handling-correctness-only'
  | 'in-try-catch'
  | 'never';
```

### `WhetherToAwait`

```ts
type WhetherToAwait = "don't-care" | 'await' | 'no-await';
```


---