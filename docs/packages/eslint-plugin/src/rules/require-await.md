[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `require-await.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 16
- **Classes**: 0
- **Imports**: 13
- **Interfaces**: 1
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/require-await.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST` | `@typescript-eslint/utils/ts-eslint` |
| `RuleFix` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getFunctionHeadLoc` | `../util` |
| `getFunctionNameWithKind` | `../util` |
| `getParserServices` | `../util` |
| `isStartOfExpressionStatement` | `../util` |
| `needsPrecedingSemicolon` | `../util` |
| `nullThrows` | `../util` |
| `upperCaseFirst` | `../util` |


---

## Functions

### `enterFunction(node: FunctionNode): void`

<details><summary>Code</summary>

```ts
function enterFunction(node: FunctionNode): void {
      scopeInfo = {
        hasAsync: node.async,
        hasAwait: false,
        isAsyncYield: false,
        isGen: node.generator || false,
        upper: scopeInfo,
      };
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Push the scope info object to the stack.
     */
```

- **Parameters**:
  - `node: FunctionNode`
- **Return Type**: `void`
### `exitFunction(node: FunctionNode): void`

<details><summary>Code</summary>

```ts
function exitFunction(node: FunctionNode): void {
      /* istanbul ignore if */ if (!scopeInfo) {
        // this shouldn't ever happen, as we have to exit a function after we enter it
        return;
      }

      if (
        node.async &&
        !scopeInfo.hasAwait &&
        !isEmptyFunction(node) &&
        !(scopeInfo.isGen && scopeInfo.isAsyncYield)
      ) {
        // If the function belongs to a method definition or
        // property, then the function's range may not include the
        // `async` keyword and we should look at the parent instead.
        const nodeWithAsyncKeyword =
          (node.parent.type === AST_NODE_TYPES.MethodDefinition &&
            node.parent.value === node) ||
          (node.parent.type === AST_NODE_TYPES.Property &&
            node.parent.method &&
            node.parent.value === node)
            ? node.parent
            : node;

        const asyncToken = nullThrows(
          context.sourceCode.getFirstToken(
            nodeWithAsyncKeyword,
            token => token.value === 'async',
          ),
          'The node is an async function, so it must have an "async" token.',
        );

        const asyncRange: Readonly<AST.Range> = [
          asyncToken.range[0],
          nullThrows(
            context.sourceCode.getTokenAfter(asyncToken, {
              includeComments: true,
            }),
            'There will always be a token after the "async" keyword.',
          ).range[0],
        ] as const;

        // Removing the `async` keyword can cause parsing errors if the
        // current statement is relying on automatic semicolon insertion.
        // If ASI is currently being used, then we should replace the
        // `async` keyword with a semicolon.
        const nextToken = nullThrows(
          context.sourceCode.getTokenAfter(asyncToken),
          'There will always be a token after the "async" keyword.',
        );
        const addSemiColon =
          nextToken.type === AST_TOKEN_TYPES.Punctuator &&
          (nextToken.value === '[' || nextToken.value === '(') &&
          (nodeWithAsyncKeyword.type === AST_NODE_TYPES.MethodDefinition ||
            isStartOfExpressionStatement(nodeWithAsyncKeyword)) &&
          needsPrecedingSemicolon(context.sourceCode, nodeWithAsyncKeyword);

        const changes = [
          { range: asyncRange, replacement: addSemiColon ? ';' : undefined },
        ];

        // If there's a return type annotation and it's a
        // `Promise<T>`, we can also change the return type
        // annotation to just `T` as part of the suggestion.
        // Alternatively, if the function is a generator and
        // the return type annotation is `AsyncGenerator<T>`,
        // then we can change it to `Generator<T>`.
        if (
          node.returnType?.typeAnnotation.type ===
          AST_NODE_TYPES.TSTypeReference
        ) {
          if (scopeInfo.isGen) {
            if (hasTypeName(node.returnType.typeAnnotation, 'AsyncGenerator')) {
              changes.push({
                range: node.returnType.typeAnnotation.typeName.range,
                replacement: 'Generator',
              });
            }
          } else if (
            hasTypeName(node.returnType.typeAnnotation, 'Promise') &&
            node.returnType.typeAnnotation.typeArguments != null
          ) {
            const openAngle = nullThrows(
              context.sourceCode.getFirstToken(
                node.returnType.typeAnnotation,
                token =>
                  token.type === AST_TOKEN_TYPES.Punctuator &&
                  token.value === '<',
              ),
              'There are type arguments, so the angle bracket will exist.',
            );
            const closeAngle = nullThrows(
              context.sourceCode.getLastToken(
                node.returnType.typeAnnotation,
                token =>
                  token.type === AST_TOKEN_TYPES.Punctuator &&
                  token.value === '>',
              ),
              'There are type arguments, so the angle bracket will exist.',
            );
            changes.push(
              // Remove the closing angled bracket.
              { range: closeAngle.range, replacement: undefined },
              // Remove the "Promise" identifier
              // and the opening angled bracket.
              {
                range: [
                  node.returnType.typeAnnotation.typeName.range[0],
                  openAngle.range[1],
                ],
                replacement: undefined,
              },
            );
          }
        }

        context.report({
          loc: getFunctionHeadLoc(node, context.sourceCode),
          node,
          messageId: 'missingAwait',
          data: {
            name: upperCaseFirst(getFunctionNameWithKind(node)),
          },
          suggest: [
            {
              messageId: 'removeAsync',
              fix: (fixer): RuleFix[] =>
                changes.map(change =>
                  change.replacement != null
                    ? fixer.replaceTextRange(change.range, change.replacement)
                    : fixer.removeRange(change.range),
                ),
            },
          ],
        });
      }

      scopeInfo = scopeInfo.upper;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Pop the top scope info object from the stack.
     * Also, it reports the function if needed.
     */
```

- **Parameters**:
  - `node: FunctionNode`
- **Return Type**: `void`
- **Calls**:
  - `isEmptyFunction`
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `context.sourceCode.getTokenAfter`
  - `isStartOfExpressionStatement (from ../util)`
  - `needsPrecedingSemicolon (from ../util)`
  - `hasTypeName`
  - `changes.push`
  - `context.sourceCode.getLastToken`
  - `context.report`
  - `getFunctionHeadLoc (from ../util)`
  - `upperCaseFirst (from ../util)`
  - `getFunctionNameWithKind (from ../util)`
  - `changes.map`
  - `fixer.replaceTextRange`
  - `fixer.removeRange`
- **Internal Comments**:
```
/* istanbul ignore if */
// this shouldn't ever happen, as we have to exit a function after we enter it
// If the function belongs to a method definition or (x2)
// property, then the function's range may not include the (x2)
// `async` keyword and we should look at the parent instead. (x2)
// Removing the `async` keyword can cause parsing errors if the (x2)
// current statement is relying on automatic semicolon insertion. (x2)
// If ASI is currently being used, then we should replace the (x2)
// `async` keyword with a semicolon. (x2)
// If there's a return type annotation and it's a
// `Promise<T>`, we can also change the return type
// annotation to just `T` as part of the suggestion.
// Alternatively, if the function is a generator and
// the return type annotation is `AsyncGenerator<T>`,
// then we can change it to `Generator<T>`.
// Remove the closing angled bracket.
// Remove the "Promise" identifier
// and the opening angled bracket.
```

### `fix(fixer: any): RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): RuleFix[] =>
                changes.map(change =>
                  change.replacement != null
                    ? fixer.replaceTextRange(change.range, change.replacement)
                    : fixer.removeRange(change.range),
                )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix[]`
- **Calls**:
  - `changes.map`
### `fix(fixer: any): RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): RuleFix[] =>
                changes.map(change =>
                  change.replacement != null
                    ? fixer.replaceTextRange(change.range, change.replacement)
                    : fixer.removeRange(change.range),
                )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix[]`
- **Calls**:
  - `changes.map`
### `fix(fixer: any): RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): RuleFix[] =>
                changes.map(change =>
                  change.replacement != null
                    ? fixer.replaceTextRange(change.range, change.replacement)
                    : fixer.removeRange(change.range),
                )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix[]`
- **Calls**:
  - `changes.map`
### `fix(fixer: any): RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): RuleFix[] =>
                changes.map(change =>
                  change.replacement != null
                    ? fixer.replaceTextRange(change.range, change.replacement)
                    : fixer.removeRange(change.range),
                )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix[]`
- **Calls**:
  - `changes.map`
### `isThenableType(node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
function isThenableType(node: ts.Node): boolean {
      const type = checker.getTypeAtLocation(node);

      return tsutils.isThenableType(checker, node, type);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the node returns a thenable type
     */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `checker.getTypeAtLocation`
  - `tsutils.isThenableType`
### `markAsHasAwait(): void`

<details><summary>Code</summary>

```ts
function markAsHasAwait(): void {
      if (!scopeInfo) {
        return;
      }
      scopeInfo.hasAwait = true;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Marks the current scope as having an await
     */
```

- **Return Type**: `void`
### `visitYieldExpression(node: TSESTree.YieldExpression): void`

<details><summary>Code</summary>

```ts
function visitYieldExpression(node: TSESTree.YieldExpression): void {
      if (!scopeInfo?.isGen || !node.argument) {
        return;
      }

      if (node.argument.type === AST_NODE_TYPES.Literal) {
        // ignoring this as for literals we don't need to check the definition
        // eg : async function* run() { yield* 1 }
        return;
      }

      if (!node.delegate) {
        if (isThenableType(services.esTreeNodeToTSNodeMap.get(node.argument))) {
          scopeInfo.isAsyncYield = true;
        }
        return;
      }

      const type = services.getTypeAtLocation(node.argument);
      const typesToCheck = expandUnionOrIntersectionType(type);
      for (const type of typesToCheck) {
        const asyncIterator = tsutils.getWellKnownSymbolPropertyOfType(
          type,
          'asyncIterator',
          checker,
        );
        if (asyncIterator != null) {
          scopeInfo.isAsyncYield = true;
          break;
        }
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Mark `scopeInfo.isAsyncYield` to `true` if it
     *  1) delegates async generator function
     *    or
     *  2) yields thenable type
     */
```

- **Parameters**:
  - `node: TSESTree.YieldExpression`
- **Return Type**: `void`
- **Calls**:
  - `isThenableType`
  - `services.esTreeNodeToTSNodeMap.get`
  - `services.getTypeAtLocation`
  - `expandUnionOrIntersectionType`
  - `tsutils.getWellKnownSymbolPropertyOfType`
- **Internal Comments**:
```
// ignoring this as for literals we don't need to check the definition
// eg : async function* run() { yield* 1 }
```

### `fix(fixer: any): RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): RuleFix[] =>
                changes.map(change =>
                  change.replacement != null
                    ? fixer.replaceTextRange(change.range, change.replacement)
                    : fixer.removeRange(change.range),
                )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix[]`
- **Calls**:
  - `changes.map`
### `fix(fixer: any): RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): RuleFix[] =>
                changes.map(change =>
                  change.replacement != null
                    ? fixer.replaceTextRange(change.range, change.replacement)
                    : fixer.removeRange(change.range),
                )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix[]`
- **Calls**:
  - `changes.map`
### `fix(fixer: any): RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): RuleFix[] =>
                changes.map(change =>
                  change.replacement != null
                    ? fixer.replaceTextRange(change.range, change.replacement)
                    : fixer.removeRange(change.range),
                )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix[]`
- **Calls**:
  - `changes.map`
### `fix(fixer: any): RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): RuleFix[] =>
                changes.map(change =>
                  change.replacement != null
                    ? fixer.replaceTextRange(change.range, change.replacement)
                    : fixer.removeRange(change.range),
                )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix[]`
- **Calls**:
  - `changes.map`
### `isEmptyFunction(node: FunctionNode): boolean`

<details><summary>Code</summary>

```ts
function isEmptyFunction(node: FunctionNode): boolean {
  return (
    node.body.type === AST_NODE_TYPES.BlockStatement &&
    node.body.body.length === 0
  );
}
```
</details>

- **Parameters**:
  - `node: FunctionNode`
- **Return Type**: `boolean`
### `expandUnionOrIntersectionType(type: ts.Type): ts.Type[]`

<details><summary>Code</summary>

```ts
function expandUnionOrIntersectionType(type: ts.Type): ts.Type[] {
  if (type.isUnionOrIntersection()) {
    return type.types.flatMap(expandUnionOrIntersectionType);
  }
  return [type];
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `ts.Type[]`
- **Calls**:
  - `type.isUnionOrIntersection`
  - `type.types.flatMap`
### `hasTypeName(typeReference: TSESTree.TSTypeReference, typeName: string): boolean`

<details><summary>Code</summary>

```ts
function hasTypeName(
  typeReference: TSESTree.TSTypeReference,
  typeName: string,
): boolean {
  return (
    typeReference.typeName.type === AST_NODE_TYPES.Identifier &&
    typeReference.typeName.name === typeName
  );
}
```
</details>

- **Parameters**:
  - `typeReference: TSESTree.TSTypeReference`
  - `typeName: string`
- **Return Type**: `boolean`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `ScopeInfo`

<details><summary>Interface Code</summary>

```ts
interface ScopeInfo {
  hasAsync: boolean;
  hasAwait: boolean;
  isAsyncYield: boolean;
  isGen: boolean;
  upper: ScopeInfo | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `hasAsync` | `boolean` | ✗ |  |
| `hasAwait` | `boolean` | ✗ |  |
| `isAsyncYield` | `boolean` | ✗ |  |
| `isGen` | `boolean` | ✗ |  |
| `upper` | `ScopeInfo | null` | ✗ |  |


---

## Type Aliases

### `FunctionNode`

```ts
type FunctionNode = | TSESTree.ArrowFunctionExpression
  | TSESTree.FunctionDeclaration
  | TSESTree.FunctionExpression;
```


---