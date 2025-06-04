[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-floating-promises.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 42 |
| 📦 Imports | 16 |
| 📊 Variables & Constants | 11 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-floating-promises.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `TypeOrValueSpecifier` | `../util` |
| `createRule` | `../util` |
| `getOperatorPrecedence` | `../util` |
| `getParserServices` | `../util` |
| `isBuiltinSymbolLike` | `../util` |
| `OperatorPrecedence` | `../util` |
| `readonlynessOptionsDefaults` | `../util` |
| `readonlynessOptionsSchema` | `../util` |
| `skipChainExpression` | `../util` |
| `typeMatchesSomeSpecifier` | `../util` |
| `parseCatchCall` | `../util/promiseUtils` |
| `parseFinallyCall` | `../util/promiseUtils` |
| `parseThenCall` | `../util/promiseUtils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `messageBase` | `"Promises must be awaited, end with a call to .catch, or end with a call to .then with a rejection handler."` | const | `'Promises must be awaited, end with a call to .catch, or end with a call to .then with a rejection handler.'` | ✗ |
| `messageBaseVoid` | `string` | const | `'Promises must be awaited, end with a call to .catch, end with a call to .then with a rejection handler' +
  ' or be explicitly marked as ignored with the `void` operator.'` | ✗ |
| `messageRejectionHandler` | `"A rejection handler that is not a function will be ignored."` | const | `'A rejection handler that is not a function will be ignored.'` | ✗ |
| `messagePromiseArray` | `"An array of Promises may be unintentional. Consider handling the promises' fulfillment or rejection with Promise.all or similar."` | const | `"An array of Promises may be unintentional. Consider handling the promises' fulfillment or rejection with Promise.all or similar."` | ✗ |
| `messagePromiseArrayVoid` | `string` | const | `"An array of Promises may be unintentional. Consider handling the promises' fulfillment or rejection with Promise.all or similar," +
  ' or explicitly marking the expression as ignored with the `void` operator.'` | ✗ |
| `allowForKnownSafePromises` | `any` | const | `options.allowForKnownSafePromises!` | ✗ |
| `allowForKnownSafeCalls` | `any` | const | `options.allowForKnownSafeCalls!` | ✗ |
| `operator` | `any` | const | `ts.isBinaryExpression(node)
        ? node.operatorToken.kind
        : ts.SyntaxKind.Unknown` | ✗ |
| `promiseHandlingMethodCall` | `{ onRejected?: any; object: TSESTree.Expression; }` | const | `parseCatchCall(node, context) ?? parseThenCall(node, context)` | ✗ |
| `onRejected` | `any` | const | `promiseHandlingMethodCall.onRejected` | ✗ |
| `arrayType` | `any` | const | `checker.getTypeArguments(ty)[0]` | ✗ |


---

## Functions

### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `addAwait(fixer: TSESLint.RuleFixer, expression: TSESTree.Expression, node: TSESTree.ExpressionStatement): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
function addAwait(
      fixer: TSESLint.RuleFixer,
      expression: TSESTree.Expression,
      node: TSESTree.ExpressionStatement,
    ): TSESLint.RuleFix | TSESLint.RuleFix[] {
      if (
        expression.type === AST_NODE_TYPES.UnaryExpression &&
        expression.operator === 'void'
      ) {
        return fixer.replaceTextRange(
          [expression.range[0], expression.range[0] + 4],
          'await',
        );
      }
      const tsNode = services.esTreeNodeToTSNodeMap.get(node.expression);
      if (isHigherPrecedenceThanUnary(tsNode)) {
        return fixer.insertTextBefore(node, 'await ');
      }
      return [
        fixer.insertTextBefore(node, 'await ('),
        fixer.insertTextAfterRange(
          [expression.range[1], expression.range[1]],
          ')',
        ),
      ];
    }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `expression: TSESTree.Expression`
  - `node: TSESTree.ExpressionStatement`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `fixer.replaceTextRange`
  - `services.esTreeNodeToTSNodeMap.get`
  - `isHigherPrecedenceThanUnary`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfterRange`
### `isKnownSafePromiseReturn(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isKnownSafePromiseReturn(node: TSESTree.Node): boolean {
      if (node.type !== AST_NODE_TYPES.CallExpression) {
        return false;
      }

      const type = services.getTypeAtLocation(node.callee);

      return typeMatchesSomeSpecifier(
        type,
        allowForKnownSafeCalls,
        services.program,
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `services.getTypeAtLocation`
  - `typeMatchesSomeSpecifier (from ../util)`
### `isHigherPrecedenceThanUnary(node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
function isHigherPrecedenceThanUnary(node: ts.Node): boolean {
      const operator = ts.isBinaryExpression(node)
        ? node.operatorToken.kind
        : ts.SyntaxKind.Unknown;
      const nodePrecedence = getOperatorPrecedence(node.kind, operator);
      return nodePrecedence > OperatorPrecedence.Unary;
    }
```
</details>

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `ts.isBinaryExpression`
  - `getOperatorPrecedence (from ../util)`
### `isAsyncIife(node: TSESTree.ExpressionStatement): boolean`

<details><summary>Code</summary>

```ts
function isAsyncIife(node: TSESTree.ExpressionStatement): boolean {
      if (node.expression.type !== AST_NODE_TYPES.CallExpression) {
        return false;
      }

      return (
        node.expression.callee.type ===
          AST_NODE_TYPES.ArrowFunctionExpression ||
        node.expression.callee.type === AST_NODE_TYPES.FunctionExpression
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.ExpressionStatement`
- **Return Type**: `boolean`
### `isValidRejectionHandler(rejectionHandler: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isValidRejectionHandler(rejectionHandler: TSESTree.Node): boolean {
      return (
        services.program
          .getTypeChecker()
          .getTypeAtLocation(
            services.esTreeNodeToTSNodeMap.get(rejectionHandler),
          )
          .getCallSignatures().length > 0
      );
    }
```
</details>

- **Parameters**:
  - `rejectionHandler: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `services.program
          .getTypeChecker()
          .getTypeAtLocation(
            services.esTreeNodeToTSNodeMap.get(rejectionHandler),
          )
          .getCallSignatures`
### `isUnhandledPromise(checker: ts.TypeChecker, node: TSESTree.Node): {
      isUnhandled: boolean;
      nonFunctionHandler?: boolean;
      promiseArray?: boolean;
    }`

<details><summary>Code</summary>

```ts
function isUnhandledPromise(
      checker: ts.TypeChecker,
      node: TSESTree.Node,
    ): {
      isUnhandled: boolean;
      nonFunctionHandler?: boolean;
      promiseArray?: boolean;
    } {
      if (node.type === AST_NODE_TYPES.AssignmentExpression) {
        return { isUnhandled: false };
      }

      // First, check expressions whose resulting types may not be promise-like
      if (node.type === AST_NODE_TYPES.SequenceExpression) {
        // Any child in a comma expression could return a potentially unhandled
        // promise, so we check them all regardless of whether the final returned
        // value is promise-like.
        return (
          node.expressions
            .map(item => isUnhandledPromise(checker, item))
            .find(result => result.isUnhandled) ?? { isUnhandled: false }
        );
      }

      if (
        !options.ignoreVoid &&
        node.type === AST_NODE_TYPES.UnaryExpression &&
        node.operator === 'void'
      ) {
        // Similarly, a `void` expression always returns undefined, so we need to
        // see what's inside it without checking the type of the overall expression.
        return isUnhandledPromise(checker, node.argument);
      }

      const tsNode = services.esTreeNodeToTSNodeMap.get(node);

      // Check the type. At this point it can't be unhandled if it isn't a promise
      // or array thereof.

      if (isPromiseArray(tsNode)) {
        return { isUnhandled: true, promiseArray: true };
      }

      // await expression addresses promises, but not promise arrays.
      if (node.type === AST_NODE_TYPES.AwaitExpression) {
        // you would think this wouldn't be strictly necessary, since we're
        // anyway checking the type of the expression, but, unfortunately TS
        // reports the result of `await (promise as Promise<number> & number)`
        // as `Promise<number> & number` instead of `number`.
        return { isUnhandled: false };
      }

      if (!isPromiseLike(tsNode)) {
        return { isUnhandled: false };
      }

      if (node.type === AST_NODE_TYPES.CallExpression) {
        // If the outer expression is a call, a `.catch()` or `.then()` with
        // rejection handler handles the promise.

        const promiseHandlingMethodCall =
          parseCatchCall(node, context) ?? parseThenCall(node, context);
        if (promiseHandlingMethodCall != null) {
          const onRejected = promiseHandlingMethodCall.onRejected;
          if (onRejected != null) {
            if (isValidRejectionHandler(onRejected)) {
              return { isUnhandled: false };
            }
            return { isUnhandled: true, nonFunctionHandler: true };
          }
          return { isUnhandled: true };
        }

        const promiseFinallyCall = parseFinallyCall(node, context);

        if (promiseFinallyCall != null) {
          return isUnhandledPromise(checker, promiseFinallyCall.object);
        }

        // All other cases are unhandled.
        return { isUnhandled: true };
      }

      if (node.type === AST_NODE_TYPES.ConditionalExpression) {
        // We must be getting the promise-like value from one of the branches of the
        // ternary. Check them directly.
        const alternateResult = isUnhandledPromise(checker, node.alternate);
        if (alternateResult.isUnhandled) {
          return alternateResult;
        }
        return isUnhandledPromise(checker, node.consequent);
      }

      if (node.type === AST_NODE_TYPES.LogicalExpression) {
        const leftResult = isUnhandledPromise(checker, node.left);
        if (leftResult.isUnhandled) {
          return leftResult;
        }
        return isUnhandledPromise(checker, node.right);
      }

      // Anything else is unhandled.
      return { isUnhandled: true };
    }
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `node: TSESTree.Node`
- **Return Type**: `{
      isUnhandled: boolean;
      nonFunctionHandler?: boolean;
      promiseArray?: boolean;
    }`
- **Calls**:
  - `node.expressions
            .map(item => isUnhandledPromise(checker, item))
            .find`
  - `isUnhandledPromise`
  - `services.esTreeNodeToTSNodeMap.get`
  - `isPromiseArray`
  - `isPromiseLike`
  - `parseCatchCall (from ../util/promiseUtils)`
  - `parseThenCall (from ../util/promiseUtils)`
  - `isValidRejectionHandler`
  - `parseFinallyCall (from ../util/promiseUtils)`
- **Internal Comments**:
```
// First, check expressions whose resulting types may not be promise-like
// Any child in a comma expression could return a potentially unhandled
// promise, so we check them all regardless of whether the final returned
// value is promise-like.
// Similarly, a `void` expression always returns undefined, so we need to
// see what's inside it without checking the type of the overall expression.
// Check the type. At this point it can't be unhandled if it isn't a promise
// or array thereof.
// await expression addresses promises, but not promise arrays.
// you would think this wouldn't be strictly necessary, since we're
// anyway checking the type of the expression, but, unfortunately TS
// reports the result of `await (promise as Promise<number> & number)`
// as `Promise<number> & number` instead of `number`.
// If the outer expression is a call, a `.catch()` or `.then()` with (x2)
// rejection handler handles the promise. (x2)
// All other cases are unhandled.
// We must be getting the promise-like value from one of the branches of the (x2)
// ternary. Check them directly. (x2)
// Anything else is unhandled.
```

### `isPromiseArray(node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
function isPromiseArray(node: ts.Node): boolean {
      const type = checker.getTypeAtLocation(node);
      for (const ty of tsutils
        .unionConstituents(type)
        .map(t => checker.getApparentType(t))) {
        if (checker.isArrayType(ty)) {
          const arrayType = checker.getTypeArguments(ty)[0];
          if (isPromiseLike(node, arrayType)) {
            return true;
          }
        }

        if (checker.isTupleType(ty)) {
          for (const tupleElementType of checker.getTypeArguments(ty)) {
            if (isPromiseLike(node, tupleElementType)) {
              return true;
            }
          }
        }
      }
      return false;
    }
```
</details>

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `checker.getTypeAtLocation`
  - `tsutils
        .unionConstituents(type)
        .map`
  - `checker.getApparentType`
  - `checker.isArrayType`
  - `checker.getTypeArguments`
  - `isPromiseLike`
  - `checker.isTupleType`
### `isPromiseLike(node: ts.Node, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isPromiseLike(node: ts.Node, type?: ts.Type): boolean {
      type ??= checker.getTypeAtLocation(node);

      // The highest priority is to allow anything allowlisted
      if (
        typeMatchesSomeSpecifier(
          type,
          allowForKnownSafePromises,
          services.program,
        )
      ) {
        return false;
      }

      // Otherwise, we always consider the built-in Promise to be Promise-like...
      const typeParts = tsutils.unionConstituents(
        checker.getApparentType(type),
      );
      if (
        typeParts.some(typePart =>
          isBuiltinSymbolLike(services.program, typePart, 'Promise'),
        )
      ) {
        return true;
      }

      // ...and only check all Thenables if explicitly told to
      if (!checkThenables) {
        return false;
      }

      // Modified from tsutils.isThenable() to only consider thenables which can be
      // rejected/caught via a second parameter. Original source (MIT licensed):
      //
      //   https://github.com/ajafff/tsutils/blob/49d0d31050b44b81e918eae4fbaf1dfe7b7286af/util/type.ts#L95-L125
      for (const ty of typeParts) {
        const then = ty.getProperty('then');
        if (then == null) {
          continue;
        }

        const thenType = checker.getTypeOfSymbolAtLocation(then, node);
        if (
          hasMatchingSignature(
            thenType,
            signature =>
              signature.parameters.length >= 2 &&
              isFunctionParam(checker, signature.parameters[0], node) &&
              isFunctionParam(checker, signature.parameters[1], node),
          )
        ) {
          return true;
        }
      }
      return false;
    }
```
</details>

- **Parameters**:
  - `node: ts.Node`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `checker.getTypeAtLocation`
  - `typeMatchesSomeSpecifier (from ../util)`
  - `tsutils.unionConstituents`
  - `checker.getApparentType`
  - `typeParts.some`
  - `isBuiltinSymbolLike (from ../util)`
  - `ty.getProperty`
  - `checker.getTypeOfSymbolAtLocation`
  - `hasMatchingSignature`
  - `isFunctionParam`
- **Internal Comments**:
```
// The highest priority is to allow anything allowlisted
// Otherwise, we always consider the built-in Promise to be Promise-like... (x2)
// ...and only check all Thenables if explicitly told to
// Modified from tsutils.isThenable() to only consider thenables which can be
// rejected/caught via a second parameter. Original source (MIT licensed):
//
//   https://github.com/ajafff/tsutils/blob/49d0d31050b44b81e918eae4fbaf1dfe7b7286af/util/type.ts#L95-L125
```

### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `fix(fixer: any): TSESLint.RuleFix | TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix | TSESLint.RuleFix[] =>
                    addAwait(fixer, expression, node)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix | TSESLint.RuleFix[]`
- **Calls**:
  - `addAwait`
### `hasMatchingSignature(type: ts.Type, matcher: (signature: ts.Signature) => boolean): boolean`

<details><summary>Code</summary>

```ts
function hasMatchingSignature(
  type: ts.Type,
  matcher: (signature: ts.Signature) => boolean,
): boolean {
  for (const t of tsutils.unionConstituents(type)) {
    if (t.getCallSignatures().some(matcher)) {
      return true;
    }
  }

  return false;
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `matcher: (signature: ts.Signature) => boolean`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.unionConstituents`
  - `t.getCallSignatures().some`
### `isFunctionParam(checker: ts.TypeChecker, param: ts.Symbol, node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
function isFunctionParam(
  checker: ts.TypeChecker,
  param: ts.Symbol,
  node: ts.Node,
): boolean {
  const type: ts.Type | undefined = checker.getApparentType(
    checker.getTypeOfSymbolAtLocation(param, node),
  );
  for (const t of tsutils.unionConstituents(type)) {
    if (t.getCallSignatures().length !== 0) {
      return true;
    }
  }
  return false;
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `param: ts.Symbol`
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `checker.getApparentType`
  - `checker.getTypeOfSymbolAtLocation`
  - `tsutils.unionConstituents`
  - `t.getCallSignatures`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    allowForKnownSafeCalls?: TypeOrValueSpecifier[];
    allowForKnownSafePromises?: TypeOrValueSpecifier[];
    checkThenables?: boolean;
    ignoreIIFE?: boolean;
    ignoreVoid?: boolean;
  },
];
```

### `MessageId`

```ts
type MessageId = | 'floating'
  | 'floatingFixAwait'
  | 'floatingFixVoid'
  | 'floatingPromiseArray'
  | 'floatingPromiseArrayVoid'
  | 'floatingUselessRejectionHandler'
  | 'floatingUselessRejectionHandlerVoid'
  | 'floatingVoid';
```


---