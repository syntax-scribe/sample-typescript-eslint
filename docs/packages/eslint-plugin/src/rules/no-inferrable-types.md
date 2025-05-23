[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-inferrable-types.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 9
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-inferrable-types.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |
| `skipChainExpression` | `../util` |


---

## Functions

### `isFunctionCall(init: TSESTree.Expression, callName: string): boolean`

<details><summary>Code</summary>

```ts
function isFunctionCall(
      init: TSESTree.Expression,
      callName: string,
    ): boolean {
      const node = skipChainExpression(init);

      return (
        node.type === AST_NODE_TYPES.CallExpression &&
        node.callee.type === AST_NODE_TYPES.Identifier &&
        node.callee.name === callName
      );
    }
```
</details>

- **Parameters**:
  - `init: TSESTree.Expression`
  - `callName: string`
- **Return Type**: `boolean`
- **Calls**:
  - `skipChainExpression (from ../util)`
### `isLiteral(init: TSESTree.Expression, typeName: string): boolean`

<details><summary>Code</summary>

```ts
function isLiteral(init: TSESTree.Expression, typeName: string): boolean {
      return (
        init.type === AST_NODE_TYPES.Literal && typeof init.value === typeName
      );
    }
```
</details>

- **Parameters**:
  - `init: TSESTree.Expression`
  - `typeName: string`
- **Return Type**: `boolean`
### `isIdentifier(init: TSESTree.Expression, names: string[]): boolean`

<details><summary>Code</summary>

```ts
function isIdentifier(
      init: TSESTree.Expression,
      ...names: string[]
    ): boolean {
      return (
        init.type === AST_NODE_TYPES.Identifier && names.includes(init.name)
      );
    }
```
</details>

- **Parameters**:
  - `init: TSESTree.Expression`
  - `names: string[]`
- **Return Type**: `boolean`
- **Calls**:
  - `names.includes`
### `hasUnaryPrefix(init: TSESTree.Expression, operators: string[]): init is TSESTree.UnaryExpression`

<details><summary>Code</summary>

```ts
function hasUnaryPrefix(
      init: TSESTree.Expression,
      ...operators: string[]
    ): init is TSESTree.UnaryExpression {
      return (
        init.type === AST_NODE_TYPES.UnaryExpression &&
        operators.includes(init.operator)
      );
    }
```
</details>

- **Parameters**:
  - `init: TSESTree.Expression`
  - `operators: string[]`
- **Return Type**: `init is TSESTree.UnaryExpression`
- **Calls**:
  - `operators.includes`
### `isInferrable(annotation: TSESTree.TypeNode, init: TSESTree.Expression): annotation is Keywords`

<details><summary>Code</summary>

```ts
function isInferrable(
      annotation: TSESTree.TypeNode,
      init: TSESTree.Expression,
    ): annotation is Keywords {
      switch (annotation.type) {
        case AST_NODE_TYPES.TSBigIntKeyword: {
          // note that bigint cannot have + prefixed to it
          const unwrappedInit = hasUnaryPrefix(init, '-')
            ? init.argument
            : init;

          return (
            isFunctionCall(unwrappedInit, 'BigInt') ||
            unwrappedInit.type === AST_NODE_TYPES.Literal
          );
        }

        case AST_NODE_TYPES.TSBooleanKeyword:
          return (
            hasUnaryPrefix(init, '!') ||
            isFunctionCall(init, 'Boolean') ||
            isLiteral(init, 'boolean')
          );

        case AST_NODE_TYPES.TSNumberKeyword: {
          const unwrappedInit = hasUnaryPrefix(init, '+', '-')
            ? init.argument
            : init;

          return (
            isIdentifier(unwrappedInit, 'Infinity', 'NaN') ||
            isFunctionCall(unwrappedInit, 'Number') ||
            isLiteral(unwrappedInit, 'number')
          );
        }

        case AST_NODE_TYPES.TSNullKeyword:
          return init.type === AST_NODE_TYPES.Literal && init.value == null;

        case AST_NODE_TYPES.TSStringKeyword:
          return (
            isFunctionCall(init, 'String') ||
            isLiteral(init, 'string') ||
            init.type === AST_NODE_TYPES.TemplateLiteral
          );

        case AST_NODE_TYPES.TSSymbolKeyword:
          return isFunctionCall(init, 'Symbol');

        case AST_NODE_TYPES.TSTypeReference: {
          if (
            annotation.typeName.type === AST_NODE_TYPES.Identifier &&
            annotation.typeName.name === 'RegExp'
          ) {
            const isRegExpLiteral =
              init.type === AST_NODE_TYPES.Literal &&
              init.value instanceof RegExp;
            const isRegExpNewCall =
              init.type === AST_NODE_TYPES.NewExpression &&
              init.callee.type === AST_NODE_TYPES.Identifier &&
              init.callee.name === 'RegExp';
            const isRegExpCall = isFunctionCall(init, 'RegExp');

            return isRegExpLiteral || isRegExpCall || isRegExpNewCall;
          }

          return false;
        }

        case AST_NODE_TYPES.TSUndefinedKeyword:
          return (
            hasUnaryPrefix(init, 'void') || isIdentifier(init, 'undefined')
          );
      }

      return false;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Returns whether a node has an inferrable value or not
     */
```

- **Parameters**:
  - `annotation: TSESTree.TypeNode`
  - `init: TSESTree.Expression`
- **Return Type**: `annotation is Keywords`
- **Calls**:
  - `hasUnaryPrefix`
  - `isFunctionCall`
  - `isLiteral`
  - `isIdentifier`
- **Internal Comments**:
```
// note that bigint cannot have + prefixed to it (x2)
```

### `reportInferrableType(node: | TSESTree.AccessorProperty
        | TSESTree.Parameter
        | TSESTree.PropertyDefinition
        | TSESTree.VariableDeclarator, typeNode: TSESTree.TSTypeAnnotation | undefined, initNode: TSESTree.Expression | null | undefined): void`

<details><summary>Code</summary>

```ts
function reportInferrableType(
      node:
        | TSESTree.AccessorProperty
        | TSESTree.Parameter
        | TSESTree.PropertyDefinition
        | TSESTree.VariableDeclarator,
      typeNode: TSESTree.TSTypeAnnotation | undefined,
      initNode: TSESTree.Expression | null | undefined,
    ): void {
      if (!typeNode || !initNode) {
        return;
      }

      if (!isInferrable(typeNode.typeAnnotation, initNode)) {
        return;
      }

      const type =
        typeNode.typeAnnotation.type === AST_NODE_TYPES.TSTypeReference
          ? // TODO - if we add more references
            'RegExp'
          : keywordMap[typeNode.typeAnnotation.type];

      context.report({
        node,
        messageId: 'noInferrableType',
        data: {
          type,
        },
        *fix(fixer) {
          if (
            (node.type === AST_NODE_TYPES.AssignmentPattern &&
              node.left.optional) ||
            (node.type === AST_NODE_TYPES.PropertyDefinition && node.definite)
          ) {
            yield fixer.remove(
              nullThrows(
                context.sourceCode.getTokenBefore(typeNode),
                NullThrowsReasons.MissingToken('token before', 'type node'),
              ),
            );
          }
          yield fixer.remove(typeNode);
        },
      });
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Reports an inferrable type declaration, if any
     */
```

- **Parameters**:
  - `node: | TSESTree.AccessorProperty
        | TSESTree.Parameter
        | TSESTree.PropertyDefinition
        | TSESTree.VariableDeclarator`
  - `typeNode: TSESTree.TSTypeAnnotation | undefined`
  - `initNode: TSESTree.Expression | null | undefined`
- **Return Type**: `void`
- **Calls**:
  - `isInferrable`
  - `context.report`
  - `fixer.remove`
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenBefore`
  - `NullThrowsReasons.MissingToken`
### `inferrableVariableVisitor(node: TSESTree.VariableDeclarator): void`

<details><summary>Code</summary>

```ts
function inferrableVariableVisitor(
      node: TSESTree.VariableDeclarator,
    ): void {
      reportInferrableType(node, node.id.typeAnnotation, node.init);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.VariableDeclarator`
- **Return Type**: `void`
- **Calls**:
  - `reportInferrableType`
### `inferrableParameterVisitor(node: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression): void`

<details><summary>Code</summary>

```ts
function inferrableParameterVisitor(
      node:
        | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression,
    ): void {
      if (ignoreParameters) {
        return;
      }

      node.params.forEach(param => {
        if (param.type === AST_NODE_TYPES.TSParameterProperty) {
          param = param.parameter;
        }

        if (param.type === AST_NODE_TYPES.AssignmentPattern) {
          reportInferrableType(param, param.left.typeAnnotation, param.right);
        }
      });
    }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `reportInferrableType`
### `inferrablePropertyVisitor(node: TSESTree.AccessorProperty | TSESTree.PropertyDefinition): void`

<details><summary>Code</summary>

```ts
function inferrablePropertyVisitor(
      node: TSESTree.AccessorProperty | TSESTree.PropertyDefinition,
    ): void {
      // We ignore `readonly` because of Microsoft/TypeScript#14416
      // Essentially a readonly property without a type
      // will result in its value being the type, leading to
      // compile errors if the type is stripped.
      if (ignoreProperties || node.readonly || node.optional) {
        return;
      }
      reportInferrableType(node, node.typeAnnotation, node.value);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorProperty | TSESTree.PropertyDefinition`
- **Return Type**: `void`
- **Calls**:
  - `reportInferrableType`
- **Internal Comments**:
```
// We ignore `readonly` because of Microsoft/TypeScript#14416
// Essentially a readonly property without a type
// will result in its value being the type, leading to
// compile errors if the type is stripped.
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
    ignoreParameters?: boolean;
    ignoreProperties?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'noInferrableType';
```

### `Keywords`

```ts
type Keywords = | TSESTree.TSBigIntKeyword
      | TSESTree.TSBooleanKeyword
      | TSESTree.TSNullKeyword
      | TSESTree.TSNumberKeyword
      | TSESTree.TSStringKeyword
      | TSESTree.TSSymbolKeyword
      | TSESTree.TSTypeReference
      | TSESTree.TSUndefinedKeyword;
```


---