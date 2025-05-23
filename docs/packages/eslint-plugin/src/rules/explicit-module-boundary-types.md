[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `explicit-module-boundary-types.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 13
- **Classes**: 0
- **Imports**: 15
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/explicit-module-boundary-types.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `DefinitionType` | `@typescript-eslint/scope-manager` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `FunctionExpression` | `../util/explicitReturnTypeUtils` |
| `FunctionInfo` | `../util/explicitReturnTypeUtils` |
| `FunctionNode` | `../util/explicitReturnTypeUtils` |
| `createRule` | `../util` |
| `hasOverloadSignatures` | `../util` |
| `isFunction` | `../util` |
| `isStaticMemberAccessOfValue` | `../util` |
| `ancestorHasReturnType` | `../util/explicitReturnTypeUtils` |
| `checkFunctionExpressionReturnType` | `../util/explicitReturnTypeUtils` |
| `checkFunctionReturnType` | `../util/explicitReturnTypeUtils` |
| `doesImmediatelyReturnFunctionExpression` | `../util/explicitReturnTypeUtils` |
| `isTypedFunctionExpression` | `../util/explicitReturnTypeUtils` |


---

## Functions

### `getReturnsInFunction(node: FunctionNode): TSESTree.ReturnStatement[]`

<details><summary>Code</summary>

```ts
function getReturnsInFunction(
      node: FunctionNode,
    ): TSESTree.ReturnStatement[] {
      return functionReturnsMap.get(node) ?? [];
    }
```
</details>

- **Parameters**:
  - `node: FunctionNode`
- **Return Type**: `TSESTree.ReturnStatement[]`
- **Calls**:
  - `functionReturnsMap.get`
### `enterFunction(node: FunctionNode): void`

<details><summary>Code</summary>

```ts
function enterFunction(node: FunctionNode): void {
      functionStack.push(node);
      functionReturnsMap.set(node, []);
    }
```
</details>

- **Parameters**:
  - `node: FunctionNode`
- **Return Type**: `void`
- **Calls**:
  - `functionStack.push`
  - `functionReturnsMap.set`
### `exitFunction(): void`

<details><summary>Code</summary>

```ts
function exitFunction(): void {
      functionStack.pop();
    }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `functionStack.pop`
### `checkParameters(node: FunctionNode | TSESTree.TSEmptyBodyFunctionExpression): void`

<details><summary>Code</summary>

```ts
function checkParameters(
      node: FunctionNode | TSESTree.TSEmptyBodyFunctionExpression,
    ): void {
      function checkParameter(param: TSESTree.Parameter): void {
        function report(
          namedMessageId: MessageIds,
          unnamedMessageId: MessageIds,
        ): void {
          if (param.type === AST_NODE_TYPES.Identifier) {
            context.report({
              node: param,
              messageId: namedMessageId,
              data: { name: param.name },
            });
          } else if (param.type === AST_NODE_TYPES.ArrayPattern) {
            context.report({
              node: param,
              messageId: unnamedMessageId,
              data: { type: 'Array pattern' },
            });
          } else if (param.type === AST_NODE_TYPES.ObjectPattern) {
            context.report({
              node: param,
              messageId: unnamedMessageId,
              data: { type: 'Object pattern' },
            });
          } else if (param.type === AST_NODE_TYPES.RestElement) {
            if (param.argument.type === AST_NODE_TYPES.Identifier) {
              context.report({
                node: param,
                messageId: namedMessageId,
                data: { name: param.argument.name },
              });
            } else {
              context.report({
                node: param,
                messageId: unnamedMessageId,
                data: { type: 'Rest' },
              });
            }
          }
        }

        switch (param.type) {
          case AST_NODE_TYPES.ArrayPattern:
          case AST_NODE_TYPES.Identifier:
          case AST_NODE_TYPES.ObjectPattern:
          case AST_NODE_TYPES.RestElement:
            if (!param.typeAnnotation) {
              report('missingArgType', 'missingArgTypeUnnamed');
            } else if (
              options.allowArgumentsExplicitlyTypedAsAny !== true &&
              param.typeAnnotation.typeAnnotation.type ===
                AST_NODE_TYPES.TSAnyKeyword
            ) {
              report('anyTypedArg', 'anyTypedArgUnnamed');
            }
            return;

          case AST_NODE_TYPES.TSParameterProperty:
            return checkParameter(param.parameter);

          case AST_NODE_TYPES.AssignmentPattern: // ignored as it has a type via its assignment
            return;
        }
      }

      for (const arg of node.params) {
        checkParameter(arg);
      }
    }
```
</details>

- **Parameters**:
  - `node: FunctionNode | TSESTree.TSEmptyBodyFunctionExpression`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `report`
  - `checkParameter`
### `checkParameter(param: TSESTree.Parameter): void`

<details><summary>Code</summary>

```ts
function checkParameter(param: TSESTree.Parameter): void {
        function report(
          namedMessageId: MessageIds,
          unnamedMessageId: MessageIds,
        ): void {
          if (param.type === AST_NODE_TYPES.Identifier) {
            context.report({
              node: param,
              messageId: namedMessageId,
              data: { name: param.name },
            });
          } else if (param.type === AST_NODE_TYPES.ArrayPattern) {
            context.report({
              node: param,
              messageId: unnamedMessageId,
              data: { type: 'Array pattern' },
            });
          } else if (param.type === AST_NODE_TYPES.ObjectPattern) {
            context.report({
              node: param,
              messageId: unnamedMessageId,
              data: { type: 'Object pattern' },
            });
          } else if (param.type === AST_NODE_TYPES.RestElement) {
            if (param.argument.type === AST_NODE_TYPES.Identifier) {
              context.report({
                node: param,
                messageId: namedMessageId,
                data: { name: param.argument.name },
              });
            } else {
              context.report({
                node: param,
                messageId: unnamedMessageId,
                data: { type: 'Rest' },
              });
            }
          }
        }

        switch (param.type) {
          case AST_NODE_TYPES.ArrayPattern:
          case AST_NODE_TYPES.Identifier:
          case AST_NODE_TYPES.ObjectPattern:
          case AST_NODE_TYPES.RestElement:
            if (!param.typeAnnotation) {
              report('missingArgType', 'missingArgTypeUnnamed');
            } else if (
              options.allowArgumentsExplicitlyTypedAsAny !== true &&
              param.typeAnnotation.typeAnnotation.type ===
                AST_NODE_TYPES.TSAnyKeyword
            ) {
              report('anyTypedArg', 'anyTypedArgUnnamed');
            }
            return;

          case AST_NODE_TYPES.TSParameterProperty:
            return checkParameter(param.parameter);

          case AST_NODE_TYPES.AssignmentPattern: // ignored as it has a type via its assignment
            return;
        }
      }
```
</details>

- **Parameters**:
  - `param: TSESTree.Parameter`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `report`
  - `checkParameter`
### `report(namedMessageId: MessageIds, unnamedMessageId: MessageIds): void`

<details><summary>Code</summary>

```ts
function report(
          namedMessageId: MessageIds,
          unnamedMessageId: MessageIds,
        ): void {
          if (param.type === AST_NODE_TYPES.Identifier) {
            context.report({
              node: param,
              messageId: namedMessageId,
              data: { name: param.name },
            });
          } else if (param.type === AST_NODE_TYPES.ArrayPattern) {
            context.report({
              node: param,
              messageId: unnamedMessageId,
              data: { type: 'Array pattern' },
            });
          } else if (param.type === AST_NODE_TYPES.ObjectPattern) {
            context.report({
              node: param,
              messageId: unnamedMessageId,
              data: { type: 'Object pattern' },
            });
          } else if (param.type === AST_NODE_TYPES.RestElement) {
            if (param.argument.type === AST_NODE_TYPES.Identifier) {
              context.report({
                node: param,
                messageId: namedMessageId,
                data: { name: param.argument.name },
              });
            } else {
              context.report({
                node: param,
                messageId: unnamedMessageId,
                data: { type: 'Rest' },
              });
            }
          }
        }
```
</details>

- **Parameters**:
  - `namedMessageId: MessageIds`
  - `unnamedMessageId: MessageIds`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
### `isAllowedName(node: TSESTree.Node | undefined): boolean`

<details><summary>Code</summary>

```ts
function isAllowedName(node: TSESTree.Node | undefined): boolean {
      if (!node || !options.allowedNames || options.allowedNames.length === 0) {
        return false;
      }

      if (
        node.type === AST_NODE_TYPES.VariableDeclarator ||
        node.type === AST_NODE_TYPES.FunctionDeclaration
      ) {
        return (
          node.id?.type === AST_NODE_TYPES.Identifier &&
          options.allowedNames.includes(node.id.name)
        );
      }

      if (
        node.type === AST_NODE_TYPES.MethodDefinition ||
        node.type === AST_NODE_TYPES.TSAbstractMethodDefinition ||
        (node.type === AST_NODE_TYPES.Property && node.method) ||
        node.type === AST_NODE_TYPES.PropertyDefinition ||
        node.type === AST_NODE_TYPES.AccessorProperty
      ) {
        return isStaticMemberAccessOfValue(
          node,
          context,
          ...options.allowedNames,
        );
      }

      return false;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if a function name is allowed and should not be checked.
     */
```

- **Parameters**:
  - `node: TSESTree.Node | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `options.allowedNames.includes`
  - `isStaticMemberAccessOfValue (from ../util)`
### `isExportedHigherOrderFunction({
      node,
    }: FunctionInfo<FunctionNode>): boolean`

<details><summary>Code</summary>

```ts
function isExportedHigherOrderFunction({
      node,
    }: FunctionInfo<FunctionNode>): boolean {
      let current: TSESTree.Node | undefined = node.parent;
      while (current) {
        if (current.type === AST_NODE_TYPES.ReturnStatement) {
          // the parent of a return will always be a block statement, so we can skip over it
          current = current.parent.parent;
          continue;
        }

        if (!isFunction(current)) {
          return false;
        }
        const returns = getReturnsInFunction(current);
        if (
          !doesImmediatelyReturnFunctionExpression({ node: current, returns })
        ) {
          return false;
        }

        if (checkedFunctions.has(current)) {
          return true;
        }

        current = current.parent;
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `{
      node,
    }: FunctionInfo<FunctionNode>`
- **Return Type**: `boolean`
- **Calls**:
  - `isFunction (from ../util)`
  - `getReturnsInFunction`
  - `doesImmediatelyReturnFunctionExpression (from ../util/explicitReturnTypeUtils)`
  - `checkedFunctions.has`
- **Internal Comments**:
```
// the parent of a return will always be a block statement, so we can skip over it (x3)
```

### `followReference(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
function followReference(node: TSESTree.Identifier): void {
      const scope = context.sourceCode.getScope(node);
      const variable = scope.set.get(node.name);
      /* istanbul ignore if */ if (!variable) {
        return;
      }

      // check all of the definitions
      for (const definition of variable.defs) {
        // cases we don't care about in this rule
        if (
          [
            DefinitionType.CatchClause,
            DefinitionType.ImplicitGlobalVariable,
            DefinitionType.ImportBinding,
            DefinitionType.Parameter,
          ].includes(definition.type)
        ) {
          continue;
        }

        checkNode(definition.node);
      }

      // follow references to find writes to the variable
      for (const reference of variable.references) {
        if (
          // we don't want to check the initialization ref, as this is handled by the declaration check
          !reference.init &&
          reference.writeExpr
        ) {
          checkNode(reference.writeExpr);
        }
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Identifier`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `scope.set.get`
  - `[
            DefinitionType.CatchClause,
            DefinitionType.ImplicitGlobalVariable,
            DefinitionType.ImportBinding,
            DefinitionType.Parameter,
          ].includes`
  - `checkNode`
- **Internal Comments**:
```
/* istanbul ignore if */
// check all of the definitions
// cases we don't care about in this rule
// follow references to find writes to the variable
// we don't want to check the initialization ref, as this is handled by the declaration check (x2)
```

### `checkNode(node: TSESTree.Node | null): void`

<details><summary>Code</summary>

```ts
function checkNode(node: TSESTree.Node | null): void {
      if (node == null || alreadyVisited.has(node)) {
        return;
      }
      alreadyVisited.add(node);

      switch (node.type) {
        case AST_NODE_TYPES.ArrowFunctionExpression:
        case AST_NODE_TYPES.FunctionExpression: {
          const returns = getReturnsInFunction(node);
          return checkFunctionExpression({ node, returns });
        }

        case AST_NODE_TYPES.ArrayExpression:
          for (const element of node.elements) {
            checkNode(element);
          }
          return;

        case AST_NODE_TYPES.PropertyDefinition:
        case AST_NODE_TYPES.AccessorProperty:
        case AST_NODE_TYPES.MethodDefinition:
        case AST_NODE_TYPES.TSAbstractMethodDefinition:
          if (
            node.accessibility === 'private' ||
            node.key.type === AST_NODE_TYPES.PrivateIdentifier
          ) {
            return;
          }
          return checkNode(node.value);

        case AST_NODE_TYPES.ClassDeclaration:
        case AST_NODE_TYPES.ClassExpression:
          for (const element of node.body.body) {
            checkNode(element);
          }
          return;

        case AST_NODE_TYPES.FunctionDeclaration: {
          const returns = getReturnsInFunction(node);
          return checkFunction({ node, returns });
        }

        case AST_NODE_TYPES.Identifier:
          return followReference(node);

        case AST_NODE_TYPES.ObjectExpression:
          for (const property of node.properties) {
            checkNode(property);
          }
          return;

        case AST_NODE_TYPES.Property:
          return checkNode(node.value);

        case AST_NODE_TYPES.TSEmptyBodyFunctionExpression:
          return checkEmptyBodyFunctionExpression(node);

        case AST_NODE_TYPES.VariableDeclaration:
          for (const declaration of node.declarations) {
            checkNode(declaration);
          }
          return;

        case AST_NODE_TYPES.VariableDeclarator:
          return checkNode(node.init);
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node | null`
- **Return Type**: `void`
- **Calls**:
  - `alreadyVisited.has`
  - `alreadyVisited.add`
  - `getReturnsInFunction`
  - `checkFunctionExpression`
  - `checkNode`
  - `checkFunction`
  - `followReference`
  - `checkEmptyBodyFunctionExpression`
### `checkEmptyBodyFunctionExpression(node: TSESTree.TSEmptyBodyFunctionExpression): void`

<details><summary>Code</summary>

```ts
function checkEmptyBodyFunctionExpression(
      node: TSESTree.TSEmptyBodyFunctionExpression,
    ): void {
      const isConstructor =
        node.parent.type === AST_NODE_TYPES.MethodDefinition &&
        node.parent.kind === 'constructor';
      const isSetAccessor =
        (node.parent.type === AST_NODE_TYPES.TSAbstractMethodDefinition ||
          node.parent.type === AST_NODE_TYPES.MethodDefinition) &&
        node.parent.kind === 'set';
      if (!isConstructor && !isSetAccessor && !node.returnType) {
        context.report({
          node,
          messageId: 'missingReturnType',
        });
      }

      checkParameters(node);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEmptyBodyFunctionExpression`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `checkParameters`
### `checkFunctionExpression({
      node,
      returns,
    }: FunctionInfo<FunctionExpression>): void`

<details><summary>Code</summary>

```ts
function checkFunctionExpression({
      node,
      returns,
    }: FunctionInfo<FunctionExpression>): void {
      if (checkedFunctions.has(node)) {
        return;
      }
      checkedFunctions.add(node);

      if (
        isAllowedName(node.parent) ||
        isTypedFunctionExpression(node, options) ||
        ancestorHasReturnType(node)
      ) {
        return;
      }

      if (
        options.allowOverloadFunctions &&
        node.parent.type === AST_NODE_TYPES.MethodDefinition &&
        hasOverloadSignatures(node.parent, context)
      ) {
        return;
      }

      checkFunctionExpressionReturnType(
        { node, returns },
        options,
        context.sourceCode,
        loc => {
          context.report({
            loc,
            node,
            messageId: 'missingReturnType',
          });
        },
      );

      checkParameters(node);
    }
```
</details>

- **Parameters**:
  - `{
      node,
      returns,
    }: FunctionInfo<FunctionExpression>`
- **Return Type**: `void`
- **Calls**:
  - `checkedFunctions.has`
  - `checkedFunctions.add`
  - `isAllowedName`
  - `isTypedFunctionExpression (from ../util/explicitReturnTypeUtils)`
  - `ancestorHasReturnType (from ../util/explicitReturnTypeUtils)`
  - `hasOverloadSignatures (from ../util)`
  - `checkFunctionExpressionReturnType (from ../util/explicitReturnTypeUtils)`
  - `context.report`
  - `checkParameters`
### `checkFunction({
      node,
      returns,
    }: FunctionInfo<TSESTree.FunctionDeclaration>): void`

<details><summary>Code</summary>

```ts
function checkFunction({
      node,
      returns,
    }: FunctionInfo<TSESTree.FunctionDeclaration>): void {
      if (checkedFunctions.has(node)) {
        return;
      }
      checkedFunctions.add(node);

      if (isAllowedName(node) || ancestorHasReturnType(node)) {
        return;
      }

      if (
        options.allowOverloadFunctions &&
        hasOverloadSignatures(node, context)
      ) {
        return;
      }

      checkFunctionReturnType(
        { node, returns },
        options,
        context.sourceCode,
        loc => {
          context.report({
            loc,
            node,
            messageId: 'missingReturnType',
          });
        },
      );

      checkParameters(node);
    }
```
</details>

- **Parameters**:
  - `{
      node,
      returns,
    }: FunctionInfo<TSESTree.FunctionDeclaration>`
- **Return Type**: `void`
- **Calls**:
  - `checkedFunctions.has`
  - `checkedFunctions.add`
  - `isAllowedName`
  - `ancestorHasReturnType (from ../util/explicitReturnTypeUtils)`
  - `hasOverloadSignatures (from ../util)`
  - `checkFunctionReturnType (from ../util/explicitReturnTypeUtils)`
  - `context.report`
  - `checkParameters`

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
    allowArgumentsExplicitlyTypedAsAny?: boolean;
    allowDirectConstAssertionInArrowFunctions?: boolean;
    allowedNames?: string[];
    allowHigherOrderFunctions?: boolean;
    allowTypedFunctionExpressions?: boolean;
    allowOverloadFunctions?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = | 'anyTypedArg'
  | 'anyTypedArgUnnamed'
  | 'missingArgType'
  | 'missingArgTypeUnnamed'
  | 'missingReturnType';
```


---