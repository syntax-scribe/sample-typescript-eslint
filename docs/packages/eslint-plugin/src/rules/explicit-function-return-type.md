[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `explicit-function-return-type.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 5
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 0
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/explicit-function-return-type.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `FunctionInfo` | `../util/explicitReturnTypeUtils` |
| `createRule` | `../util` |
| `nullThrows` | `../util` |
| `ancestorHasReturnType` | `../util/explicitReturnTypeUtils` |
| `checkFunctionReturnType` | `../util/explicitReturnTypeUtils` |
| `isValidFunctionExpressionReturnType` | `../util/explicitReturnTypeUtils` |


---

## Functions

### `enterFunction(node: FunctionNode): void`

<details><summary>Code</summary>

```ts
function enterFunction(node: FunctionNode): void {
      functionInfoStack.push({
        node,
        returns: [],
      });
    }
```
</details>

- **Parameters**:
  - `node: FunctionNode`
- **Return Type**: `void`
- **Calls**:
  - `functionInfoStack.push`
### `popFunctionInfo(exitNodeType: string): FunctionInfo<FunctionNode>`

<details><summary>Code</summary>

```ts
function popFunctionInfo(exitNodeType: string): FunctionInfo<FunctionNode> {
      return nullThrows(
        functionInfoStack.pop(),
        `Stack should exist on ${exitNodeType} exit`,
      );
    }
```
</details>

- **Parameters**:
  - `exitNodeType: string`
- **Return Type**: `FunctionInfo<FunctionNode>`
- **Calls**:
  - `nullThrows (from ../util)`
  - `functionInfoStack.pop`
### `isAllowedFunction(node: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression): boolean`

<details><summary>Code</summary>

```ts
function isAllowedFunction(
      node:
        | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression,
    ): boolean {
      if (options.allowFunctionsWithoutTypeParameters && !node.typeParameters) {
        return true;
      }

      if (options.allowIIFEs && isIIFE(node)) {
        return true;
      }

      if (!options.allowedNames?.length) {
        return false;
      }

      if (
        node.type === AST_NODE_TYPES.ArrowFunctionExpression ||
        node.type === AST_NODE_TYPES.FunctionExpression
      ) {
        const parent = node.parent;
        let funcName;
        if (node.id?.name) {
          funcName = node.id.name;
        } else {
          switch (parent.type) {
            case AST_NODE_TYPES.VariableDeclarator: {
              if (parent.id.type === AST_NODE_TYPES.Identifier) {
                funcName = parent.id.name;
              }
              break;
            }
            case AST_NODE_TYPES.MethodDefinition:
            case AST_NODE_TYPES.PropertyDefinition:
            case AST_NODE_TYPES.Property: {
              if (
                parent.key.type === AST_NODE_TYPES.Identifier &&
                !parent.computed
              ) {
                funcName = parent.key.name;
              }
              break;
            }
          }
        }
        if (!!funcName && options.allowedNames.includes(funcName)) {
          return true;
        }
      }
      if (
        node.type === AST_NODE_TYPES.FunctionDeclaration &&
        node.id &&
        options.allowedNames.includes(node.id.name)
      ) {
        return true;
      }
      return false;
    }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `isIIFE`
  - `options.allowedNames.includes`
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
      return node.parent.type === AST_NODE_TYPES.CallExpression;
    }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression`
- **Return Type**: `boolean`
### `exitFunctionExpression(node: TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression): void`

<details><summary>Code</summary>

```ts
function exitFunctionExpression(
      node: TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression,
    ): void {
      const info = popFunctionInfo('function expression');

      if (
        options.allowConciseArrowFunctionExpressionsStartingWithVoid &&
        node.type === AST_NODE_TYPES.ArrowFunctionExpression &&
        node.expression &&
        node.body.type === AST_NODE_TYPES.UnaryExpression &&
        node.body.operator === 'void'
      ) {
        return;
      }

      if (isAllowedFunction(node)) {
        return;
      }

      if (
        options.allowTypedFunctionExpressions &&
        (isValidFunctionExpressionReturnType(node, options) ||
          ancestorHasReturnType(node))
      ) {
        return;
      }

      checkFunctionReturnType(info, options, context.sourceCode, loc =>
        context.report({
          loc,
          node,
          messageId: 'missingReturnType',
        }),
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression`
- **Return Type**: `void`
- **Calls**:
  - `popFunctionInfo`
  - `isAllowedFunction`
  - `isValidFunctionExpressionReturnType (from ../util/explicitReturnTypeUtils)`
  - `ancestorHasReturnType (from ../util/explicitReturnTypeUtils)`
  - `checkFunctionReturnType (from ../util/explicitReturnTypeUtils)`
  - `context.report`

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
    allowConciseArrowFunctionExpressionsStartingWithVoid?: boolean;
    allowDirectConstAssertionInArrowFunctions?: boolean;
    allowedNames?: string[];
    allowExpressions?: boolean;
    allowFunctionsWithoutTypeParameters?: boolean;
    allowHigherOrderFunctions?: boolean;
    allowIIFEs?: boolean;
    allowTypedFunctionExpressions?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'missingReturnType';
```

### `FunctionNode`

```ts
type FunctionNode = | TSESTree.ArrowFunctionExpression
  | TSESTree.FunctionDeclaration
  | TSESTree.FunctionExpression;
```


---