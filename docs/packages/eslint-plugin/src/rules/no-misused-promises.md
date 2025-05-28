[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-misused-promises.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 26 |
| 🧱 Classes | 0 |
| 📦 Imports | 11 |
| 📊 Variables & Constants | 15 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-misused-promises.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getFunctionHeadLoc` | `../util` |
| `getParserServices` | `../util` |
| `isArrayMethodCallWithPredicate` | `../util` |
| `isFunction` | `../util` |
| `isRestParameterDeclaration` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `checkedNodes` | `Set<TSESTree.Node>` | const | `new Set<TSESTree.Node>()` | ✗ |
| `conditionalChecks` | `TSESLint.RuleListener` | const | `{
      'CallExpression > MemberExpression': checkArrayPredicates,
      ConditionalExpression: checkTestConditional,
      DoWhileStatement: checkTestConditional,
      ForStatement: checkTestConditional,
      IfStatement: checkTestConditional,
      LogicalExpression: checkConditional,
      'UnaryExpression[operator="!"]'(node: TSESTree.UnaryExpression) {
        checkConditional(node.argument, true);
      },
      WhileStatement: checkTestConditional,
    }` | ✗ |
| `voidReturnChecks` | `TSESLint.RuleListener` | const | `checksVoidReturn
      ? {
          ...(checksVoidReturn.arguments && {
            CallExpression: checkArguments,
            NewExpression: checkArguments,
          }),
          ...(checksVoidReturn.attributes && {
            JSXAttribute: checkJSXAttribute,
          }),
          ...(checksVoidReturn.inheritedMethods && {
            ClassDeclaration: checkClassLikeOrInterfaceNode,
            ClassExpression: checkClassLikeOrInterfaceNode,
            TSInterfaceDeclaration: checkClassLikeOrInterfaceNode,
          }),
          ...(checksVoidReturn.properties && {
            Property: checkProperty,
          }),
          ...(checksVoidReturn.returns && {
            ReturnStatement: checkReturnStatement,
          }),
          ...(checksVoidReturn.variables && {
            AssignmentExpression: checkAssignment,
            VariableDeclarator: checkVariableDeclaration,
          }),
        }
      : {}` | ✗ |
| `spreadChecks` | `TSESLint.RuleListener` | const | `{
      SpreadElement: checkSpread,
    }` | ✗ |
| `parent` | `any` | const | `node.parent` | ✗ |
| `functionNode` | `any` | const | `node.value` | ✗ |
| `obj` | `any` | const | `tsNode.parent` | ✗ |
| `functionNode` | `TSESTree.FunctionExpression` | const | `node.value as TSESTree.FunctionExpression` | ✗ |
| `current` | `TSESTree.Node | undefined` | let/var | `node.parent` | ✗ |
| `hasThenableSignature` | `boolean` | let/var | `false` | ✗ |
| `thenableReturnIndices` | `Set<number>` | const | `new Set<number>()` | ✗ |
| `voidReturnIndices` | `Set<number>` | const | `new Set<number>()` | ✗ |
| `signatures` | `any` | const | `ts.isCallExpression(node)
      ? subType.getCallSignatures()
      : subType.getConstructSignatures()` | ✗ |
| `decl` | `any` | const | `parameter.valueDeclaration` | ✗ |
| `hadVoidReturn` | `boolean` | let/var | `false` | ✗ |


---

## Functions

### `parseChecksVoidReturn(checksVoidReturn: boolean | ChecksVoidReturnOptions | undefined): ChecksVoidReturnOptions | false`

<details><summary>Code</summary>

```ts
function parseChecksVoidReturn(
  checksVoidReturn: boolean | ChecksVoidReturnOptions | undefined,
): ChecksVoidReturnOptions | false {
  switch (checksVoidReturn) {
    case false:
      return false;

    case true:
    case undefined:
      return {
        arguments: true,
        attributes: true,
        inheritedMethods: true,
        properties: true,
        returns: true,
        variables: true,
      };

    default:
      return {
        arguments: checksVoidReturn.arguments ?? true,
        attributes: checksVoidReturn.attributes ?? true,
        inheritedMethods: checksVoidReturn.inheritedMethods ?? true,
        properties: checksVoidReturn.properties ?? true,
        returns: checksVoidReturn.returns ?? true,
        variables: checksVoidReturn.variables ?? true,
      };
  }
}
```
</details>

- **Parameters**:
  - `checksVoidReturn: boolean | ChecksVoidReturnOptions | undefined`
- **Return Type**: `ChecksVoidReturnOptions | false`
### `isPossiblyFunctionType(node: TSESTree.TSTypeAnnotation): boolean`

<details><summary>Code</summary>

```ts
function isPossiblyFunctionType(node: TSESTree.TSTypeAnnotation): boolean {
      switch (node.typeAnnotation.type) {
        case AST_NODE_TYPES.TSConditionalType:
        case AST_NODE_TYPES.TSConstructorType:
        case AST_NODE_TYPES.TSFunctionType:
        case AST_NODE_TYPES.TSImportType:
        case AST_NODE_TYPES.TSIndexedAccessType:
        case AST_NODE_TYPES.TSInferType:
        case AST_NODE_TYPES.TSIntersectionType:
        case AST_NODE_TYPES.TSQualifiedName:
        case AST_NODE_TYPES.TSThisType:
        case AST_NODE_TYPES.TSTypeOperator:
        case AST_NODE_TYPES.TSTypeQuery:
        case AST_NODE_TYPES.TSTypeReference:
        case AST_NODE_TYPES.TSUnionType:
          return true;

        case AST_NODE_TYPES.TSTypeLiteral:
          return node.typeAnnotation.members.some(
            member =>
              member.type === AST_NODE_TYPES.TSCallSignatureDeclaration ||
              member.type === AST_NODE_TYPES.TSConstructSignatureDeclaration,
          );

        case AST_NODE_TYPES.TSAbstractKeyword:
        case AST_NODE_TYPES.TSAnyKeyword:
        case AST_NODE_TYPES.TSArrayType:
        case AST_NODE_TYPES.TSAsyncKeyword:
        case AST_NODE_TYPES.TSBigIntKeyword:
        case AST_NODE_TYPES.TSBooleanKeyword:
        case AST_NODE_TYPES.TSDeclareKeyword:
        case AST_NODE_TYPES.TSExportKeyword:
        case AST_NODE_TYPES.TSIntrinsicKeyword:
        case AST_NODE_TYPES.TSLiteralType:
        case AST_NODE_TYPES.TSMappedType:
        case AST_NODE_TYPES.TSNamedTupleMember:
        case AST_NODE_TYPES.TSNeverKeyword:
        case AST_NODE_TYPES.TSNullKeyword:
        case AST_NODE_TYPES.TSNumberKeyword:
        case AST_NODE_TYPES.TSObjectKeyword:
        case AST_NODE_TYPES.TSOptionalType:
        case AST_NODE_TYPES.TSPrivateKeyword:
        case AST_NODE_TYPES.TSProtectedKeyword:
        case AST_NODE_TYPES.TSPublicKeyword:
        case AST_NODE_TYPES.TSReadonlyKeyword:
        case AST_NODE_TYPES.TSRestType:
        case AST_NODE_TYPES.TSStaticKeyword:
        case AST_NODE_TYPES.TSStringKeyword:
        case AST_NODE_TYPES.TSSymbolKeyword:
        case AST_NODE_TYPES.TSTemplateLiteralType:
        case AST_NODE_TYPES.TSTupleType:
        case AST_NODE_TYPES.TSTypePredicate:
        case AST_NODE_TYPES.TSUndefinedKeyword:
        case AST_NODE_TYPES.TSUnknownKeyword:
        case AST_NODE_TYPES.TSVoidKeyword:
          return false;
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * A syntactic check to see if an annotated type is maybe a function type.
     * This is a perf optimization to help avoid requesting types where possible
     */
```

- **Parameters**:
  - `node: TSESTree.TSTypeAnnotation`
- **Return Type**: `boolean`
- **Calls**:
  - `node.typeAnnotation.members.some`
### `checkTestConditional(node: | TSESTree.ConditionalExpression
        | TSESTree.DoWhileStatement
        | TSESTree.ForStatement
        | TSESTree.IfStatement
        | TSESTree.WhileStatement): void`

<details><summary>Code</summary>

```ts
function checkTestConditional(
      node:
        | TSESTree.ConditionalExpression
        | TSESTree.DoWhileStatement
        | TSESTree.ForStatement
        | TSESTree.IfStatement
        | TSESTree.WhileStatement,
    ): void {
      if (node.test) {
        checkConditional(node.test, true);
      }
    }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ConditionalExpression
        | TSESTree.DoWhileStatement
        | TSESTree.ForStatement
        | TSESTree.IfStatement
        | TSESTree.WhileStatement`
- **Return Type**: `void`
- **Calls**:
  - `checkConditional`
### `checkConditional(node: TSESTree.Expression, isTestExpr: boolean): void`

<details><summary>Code</summary>

```ts
function checkConditional(
      node: TSESTree.Expression,
      isTestExpr = false,
    ): void {
      // prevent checking the same node multiple times
      if (checkedNodes.has(node)) {
        return;
      }
      checkedNodes.add(node);

      if (node.type === AST_NODE_TYPES.LogicalExpression) {
        // ignore the left operand for nullish coalescing expressions not in a context of a test expression
        if (node.operator !== '??' || isTestExpr) {
          checkConditional(node.left, isTestExpr);
        }
        // we ignore the right operand when not in a context of a test expression
        if (isTestExpr) {
          checkConditional(node.right, isTestExpr);
        }
        return;
      }
      const tsNode = services.esTreeNodeToTSNodeMap.get(node);
      if (isAlwaysThenable(checker, tsNode)) {
        context.report({
          node,
          messageId: 'conditional',
        });
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * This function analyzes the type of a node and checks if it is a Promise in a boolean conditional.
     * It uses recursion when checking nested logical operators.
     * @param node The AST node to check.
     * @param isTestExpr Whether the node is a descendant of a test expression.
     */
```

- **Parameters**:
  - `node: TSESTree.Expression`
  - `isTestExpr: boolean`
- **Return Type**: `void`
- **Calls**:
  - `checkedNodes.has`
  - `checkedNodes.add`
  - `checkConditional`
  - `services.esTreeNodeToTSNodeMap.get`
  - `isAlwaysThenable`
  - `context.report`
- **Internal Comments**:
```
// prevent checking the same node multiple times
// ignore the left operand for nullish coalescing expressions not in a context of a test expression
// we ignore the right operand when not in a context of a test expression
```

### `checkArrayPredicates(node: TSESTree.MemberExpression): void`

<details><summary>Code</summary>

```ts
function checkArrayPredicates(node: TSESTree.MemberExpression): void {
      const parent = node.parent;
      if (parent.type === AST_NODE_TYPES.CallExpression) {
        const callback = parent.arguments.at(0);
        if (
          callback &&
          isArrayMethodCallWithPredicate(context, services, parent)
        ) {
          const type = services.esTreeNodeToTSNodeMap.get(callback);
          if (returnsThenable(checker, type)) {
            context.report({
              node: callback,
              messageId: 'predicate',
            });
          }
        }
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.MemberExpression`
- **Return Type**: `void`
- **Calls**:
  - `parent.arguments.at`
  - `isArrayMethodCallWithPredicate (from ../util)`
  - `services.esTreeNodeToTSNodeMap.get`
  - `returnsThenable`
  - `context.report`
### `checkArguments(node: TSESTree.CallExpression | TSESTree.NewExpression): void`

<details><summary>Code</summary>

```ts
function checkArguments(
      node: TSESTree.CallExpression | TSESTree.NewExpression,
    ): void {
      const tsNode = services.esTreeNodeToTSNodeMap.get(node);
      const voidArgs = voidFunctionArguments(checker, tsNode);
      if (voidArgs.size === 0) {
        return;
      }

      for (const [index, argument] of node.arguments.entries()) {
        if (!voidArgs.has(index)) {
          continue;
        }

        const tsNode = services.esTreeNodeToTSNodeMap.get(argument);
        if (returnsThenable(checker, tsNode as ts.Expression)) {
          context.report({
            node: argument,
            messageId: 'voidReturnArgument',
          });
        }
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression | TSESTree.NewExpression`
- **Return Type**: `void`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `voidFunctionArguments`
  - `node.arguments.entries`
  - `voidArgs.has`
  - `returnsThenable`
  - `context.report`
### `checkAssignment(node: TSESTree.AssignmentExpression): void`

<details><summary>Code</summary>

```ts
function checkAssignment(node: TSESTree.AssignmentExpression): void {
      const tsNode = services.esTreeNodeToTSNodeMap.get(node);
      const varType = services.getTypeAtLocation(node.left);
      if (!isVoidReturningFunctionType(checker, tsNode.left, varType)) {
        return;
      }

      if (returnsThenable(checker, tsNode.right)) {
        context.report({
          node: node.right,
          messageId: 'voidReturnVariable',
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.AssignmentExpression`
- **Return Type**: `void`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `services.getTypeAtLocation`
  - `isVoidReturningFunctionType`
  - `returnsThenable`
  - `context.report`
### `checkVariableDeclaration(node: TSESTree.VariableDeclarator): void`

<details><summary>Code</summary>

```ts
function checkVariableDeclaration(node: TSESTree.VariableDeclarator): void {
      const tsNode = services.esTreeNodeToTSNodeMap.get(node);
      if (
        tsNode.initializer == null ||
        node.init == null ||
        node.id.typeAnnotation == null
      ) {
        return;
      }

      // syntactically ignore some known-good cases to avoid touching type info
      if (!isPossiblyFunctionType(node.id.typeAnnotation)) {
        return;
      }

      const varType = services.getTypeAtLocation(node.id);
      if (!isVoidReturningFunctionType(checker, tsNode.initializer, varType)) {
        return;
      }

      if (returnsThenable(checker, tsNode.initializer)) {
        context.report({
          node: node.init,
          messageId: 'voidReturnVariable',
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.VariableDeclarator`
- **Return Type**: `void`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `isPossiblyFunctionType`
  - `services.getTypeAtLocation`
  - `isVoidReturningFunctionType`
  - `returnsThenable`
  - `context.report`
- **Internal Comments**:
```
// syntactically ignore some known-good cases to avoid touching type info
```

### `checkProperty(node: TSESTree.Property): void`

<details><summary>Code</summary>

```ts
function checkProperty(node: TSESTree.Property): void {
      const tsNode = services.esTreeNodeToTSNodeMap.get(node);
      if (ts.isPropertyAssignment(tsNode)) {
        const contextualType = checker.getContextualType(tsNode.initializer);
        if (
          contextualType != null &&
          isVoidReturningFunctionType(
            checker,
            tsNode.initializer,
            contextualType,
          ) &&
          returnsThenable(checker, tsNode.initializer)
        ) {
          if (isFunction(node.value)) {
            const functionNode = node.value;
            if (functionNode.returnType) {
              context.report({
                node: functionNode.returnType.typeAnnotation,
                messageId: 'voidReturnProperty',
              });
            } else {
              context.report({
                loc: getFunctionHeadLoc(functionNode, context.sourceCode),
                messageId: 'voidReturnProperty',
              });
            }
          } else {
            context.report({
              node: node.value,
              messageId: 'voidReturnProperty',
            });
          }
        }
      } else if (ts.isShorthandPropertyAssignment(tsNode)) {
        const contextualType = checker.getContextualType(tsNode.name);
        if (
          contextualType != null &&
          isVoidReturningFunctionType(checker, tsNode.name, contextualType) &&
          returnsThenable(checker, tsNode.name)
        ) {
          context.report({
            node: node.value,
            messageId: 'voidReturnProperty',
          });
        }
      } else if (ts.isMethodDeclaration(tsNode)) {
        if (ts.isComputedPropertyName(tsNode.name)) {
          return;
        }
        const obj = tsNode.parent;

        // Below condition isn't satisfied unless something goes wrong,
        // but is needed for type checking.
        // 'node' does not include class method declaration so 'obj' is
        // always an object literal expression, but after converting 'node'
        // to TypeScript AST, its type includes MethodDeclaration which
        // does include the case of class method declaration.
        if (!ts.isObjectLiteralExpression(obj)) {
          return;
        }

        if (!returnsThenable(checker, tsNode)) {
          return;
        }
        const objType = checker.getContextualType(obj);
        if (objType == null) {
          return;
        }
        const propertySymbol = checker.getPropertyOfType(
          objType,
          tsNode.name.text,
        );
        if (propertySymbol == null) {
          return;
        }

        const contextualType = checker.getTypeOfSymbolAtLocation(
          propertySymbol,
          tsNode.name,
        );

        if (isVoidReturningFunctionType(checker, tsNode.name, contextualType)) {
          const functionNode = node.value as TSESTree.FunctionExpression;

          if (functionNode.returnType) {
            context.report({
              node: functionNode.returnType.typeAnnotation,
              messageId: 'voidReturnProperty',
            });
          } else {
            context.report({
              loc: getFunctionHeadLoc(functionNode, context.sourceCode),
              messageId: 'voidReturnProperty',
            });
          }
        }
        return;
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Property`
- **Return Type**: `void`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `ts.isPropertyAssignment`
  - `checker.getContextualType`
  - `isVoidReturningFunctionType`
  - `returnsThenable`
  - `isFunction (from ../util)`
  - `context.report`
  - `getFunctionHeadLoc (from ../util)`
  - `ts.isShorthandPropertyAssignment`
  - `ts.isMethodDeclaration`
  - `ts.isComputedPropertyName`
  - `ts.isObjectLiteralExpression`
  - `checker.getPropertyOfType`
  - `checker.getTypeOfSymbolAtLocation`
- **Internal Comments**:
```
// Below condition isn't satisfied unless something goes wrong,
// but is needed for type checking.
// 'node' does not include class method declaration so 'obj' is
// always an object literal expression, but after converting 'node'
// to TypeScript AST, its type includes MethodDeclaration which
// does include the case of class method declaration.
```

### `checkReturnStatement(node: TSESTree.ReturnStatement): void`

<details><summary>Code</summary>

```ts
function checkReturnStatement(node: TSESTree.ReturnStatement): void {
      const tsNode = services.esTreeNodeToTSNodeMap.get(node);
      if (tsNode.expression == null || node.argument == null) {
        return;
      }

      // syntactically ignore some known-good cases to avoid touching type info
      const functionNode = (() => {
        let current: TSESTree.Node | undefined = node.parent;
        while (current && !isFunction(current)) {
          current = current.parent;
        }
        return nullThrows(current, NullThrowsReasons.MissingParent);
      })();

      if (
        functionNode.returnType &&
        !isPossiblyFunctionType(functionNode.returnType)
      ) {
        return;
      }

      const contextualType = checker.getContextualType(tsNode.expression);
      if (
        contextualType != null &&
        isVoidReturningFunctionType(
          checker,
          tsNode.expression,
          contextualType,
        ) &&
        returnsThenable(checker, tsNode.expression)
      ) {
        context.report({
          node: node.argument,
          messageId: 'voidReturnReturnValue',
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.ReturnStatement`
- **Return Type**: `void`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `complex_call_18240`
  - `isFunction (from ../util)`
  - `nullThrows (from ../util)`
  - `isPossiblyFunctionType`
  - `checker.getContextualType`
  - `isVoidReturningFunctionType`
  - `returnsThenable`
  - `context.report`
- **Internal Comments**:
```
// syntactically ignore some known-good cases to avoid touching type info (x2)
```

### `checkClassLikeOrInterfaceNode(node: | TSESTree.ClassDeclaration
        | TSESTree.ClassExpression
        | TSESTree.TSInterfaceDeclaration): void`

<details><summary>Code</summary>

```ts
function checkClassLikeOrInterfaceNode(
      node:
        | TSESTree.ClassDeclaration
        | TSESTree.ClassExpression
        | TSESTree.TSInterfaceDeclaration,
    ): void {
      const tsNode = services.esTreeNodeToTSNodeMap.get(node);

      const heritageTypes = getHeritageTypes(checker, tsNode);
      if (!heritageTypes?.length) {
        return;
      }

      for (const nodeMember of tsNode.members) {
        const memberName = nodeMember.name?.getText();
        if (memberName == null) {
          // Call/construct/index signatures don't have names. TS allows call signatures to mismatch,
          // and construct signatures can't be async.
          // TODO - Once we're able to use `checker.isTypeAssignableTo` (v8), we can check an index
          // signature here against its compatible index signatures in `heritageTypes`
          continue;
        }
        if (!returnsThenable(checker, nodeMember)) {
          continue;
        }

        const node = services.tsNodeToESTreeNodeMap.get(nodeMember);
        if (isStaticMember(node)) {
          continue;
        }

        for (const heritageType of heritageTypes) {
          checkHeritageTypeForMemberReturningVoid(
            nodeMember,
            heritageType,
            memberName,
          );
        }
      }
    }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ClassDeclaration
        | TSESTree.ClassExpression
        | TSESTree.TSInterfaceDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `getHeritageTypes`
  - `nodeMember.name?.getText`
  - `returnsThenable`
  - `services.tsNodeToESTreeNodeMap.get`
  - `isStaticMember`
  - `checkHeritageTypeForMemberReturningVoid`
- **Internal Comments**:
```
// Call/construct/index signatures don't have names. TS allows call signatures to mismatch,
// and construct signatures can't be async.
// TODO - Once we're able to use `checker.isTypeAssignableTo` (v8), we can check an index
// signature here against its compatible index signatures in `heritageTypes`
```

### `checkHeritageTypeForMemberReturningVoid(nodeMember: ts.Node, heritageType: ts.Type, memberName: string): void`

<details><summary>Code</summary>

```ts
function checkHeritageTypeForMemberReturningVoid(
      nodeMember: ts.Node,
      heritageType: ts.Type,
      memberName: string,
    ): void {
      const heritageMember = getMemberIfExists(heritageType, memberName);
      if (heritageMember == null) {
        return;
      }
      const memberType = checker.getTypeOfSymbolAtLocation(
        heritageMember,
        nodeMember,
      );
      if (!isVoidReturningFunctionType(checker, nodeMember, memberType)) {
        return;
      }
      context.report({
        node: services.tsNodeToESTreeNodeMap.get(nodeMember),
        messageId: 'voidReturnInheritedMethod',
        data: { heritageTypeName: checker.typeToString(heritageType) },
      });
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks `heritageType` for a member named `memberName` that returns void; reports the
     * 'voidReturnInheritedMethod' message if found.
     * @param nodeMember Node member that returns a Promise
     * @param heritageType Heritage type to check against
     * @param memberName Name of the member to check for
     */
```

- **Parameters**:
  - `nodeMember: ts.Node`
  - `heritageType: ts.Type`
  - `memberName: string`
- **Return Type**: `void`
- **Calls**:
  - `getMemberIfExists`
  - `checker.getTypeOfSymbolAtLocation`
  - `isVoidReturningFunctionType`
  - `context.report`
  - `services.tsNodeToESTreeNodeMap.get`
  - `checker.typeToString`
### `checkJSXAttribute(node: TSESTree.JSXAttribute): void`

<details><summary>Code</summary>

```ts
function checkJSXAttribute(node: TSESTree.JSXAttribute): void {
      if (
        node.value == null ||
        node.value.type !== AST_NODE_TYPES.JSXExpressionContainer
      ) {
        return;
      }
      const expressionContainer = services.esTreeNodeToTSNodeMap.get(
        node.value,
      );
      const expression = services.esTreeNodeToTSNodeMap.get(
        node.value.expression,
      );
      const contextualType = checker.getContextualType(expressionContainer);
      if (
        contextualType != null &&
        isVoidReturningFunctionType(
          checker,
          expressionContainer,
          contextualType,
        ) &&
        returnsThenable(checker, expression)
      ) {
        context.report({
          node: node.value,
          messageId: 'voidReturnAttribute',
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.JSXAttribute`
- **Return Type**: `void`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `checker.getContextualType`
  - `isVoidReturningFunctionType`
  - `returnsThenable`
  - `context.report`
### `checkSpread(node: TSESTree.SpreadElement): void`

<details><summary>Code</summary>

```ts
function checkSpread(node: TSESTree.SpreadElement): void {
      const tsNode = services.esTreeNodeToTSNodeMap.get(node);

      if (isSometimesThenable(checker, tsNode.expression)) {
        context.report({
          node: node.argument,
          messageId: 'spread',
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.SpreadElement`
- **Return Type**: `void`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `isSometimesThenable`
  - `context.report`
### `isSometimesThenable(checker: ts.TypeChecker, node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
function isSometimesThenable(checker: ts.TypeChecker, node: ts.Node): boolean {
  const type = checker.getTypeAtLocation(node);

  for (const subType of tsutils.unionConstituents(
    checker.getApparentType(type),
  )) {
    if (tsutils.isThenableType(checker, node, subType)) {
      return true;
    }
  }

  return false;
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `checker.getTypeAtLocation`
  - `tsutils.unionConstituents`
  - `checker.getApparentType`
  - `tsutils.isThenableType`
### `isAlwaysThenable(checker: ts.TypeChecker, node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
function isAlwaysThenable(checker: ts.TypeChecker, node: ts.Node): boolean {
  const type = checker.getTypeAtLocation(node);

  for (const subType of tsutils.unionConstituents(
    checker.getApparentType(type),
  )) {
    const thenProp = subType.getProperty('then');

    // If one of the alternates has no then property, it is not thenable in all
    // cases.
    if (thenProp == null) {
      return false;
    }

    // We walk through each variation of the then property. Since we know it
    // exists at this point, we just need at least one of the alternates to
    // be of the right form to consider it thenable.
    const thenType = checker.getTypeOfSymbolAtLocation(thenProp, node);
    let hasThenableSignature = false;
    for (const subType of tsutils.unionConstituents(thenType)) {
      for (const signature of subType.getCallSignatures()) {
        if (
          signature.parameters.length !== 0 &&
          isFunctionParam(checker, signature.parameters[0], node)
        ) {
          hasThenableSignature = true;
          break;
        }
      }

      // We only need to find one variant of the then property that has a
      // function signature for it to be thenable.
      if (hasThenableSignature) {
        break;
      }
    }

    // If no flavors of the then property are thenable, we don't consider the
    // overall type to be thenable
    if (!hasThenableSignature) {
      return false;
    }
  }

  // If all variants are considered thenable (i.e. haven't returned false), we
  // consider the overall type thenable
  return true;
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `checker.getTypeAtLocation`
  - `tsutils.unionConstituents`
  - `checker.getApparentType`
  - `subType.getProperty`
  - `checker.getTypeOfSymbolAtLocation`
  - `subType.getCallSignatures`
  - `isFunctionParam`
- **Internal Comments**:
```
// If one of the alternates has no then property, it is not thenable in all
// cases.
// We walk through each variation of the then property. Since we know it (x2)
// exists at this point, we just need at least one of the alternates to (x2)
// be of the right form to consider it thenable. (x2)
// We only need to find one variant of the then property that has a
// function signature for it to be thenable.
// If no flavors of the then property are thenable, we don't consider the
// overall type to be thenable
// If all variants are considered thenable (i.e. haven't returned false), we
// consider the overall type thenable
```

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
  for (const subType of tsutils.unionConstituents(type)) {
    if (subType.getCallSignatures().length !== 0) {
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
  - `subType.getCallSignatures`
### `checkThenableOrVoidArgument(checker: ts.TypeChecker, node: ts.CallExpression | ts.NewExpression, type: ts.Type, index: number, thenableReturnIndices: Set<number>, voidReturnIndices: Set<number>): void`

<details><summary>Code</summary>

```ts
function checkThenableOrVoidArgument(
  checker: ts.TypeChecker,
  node: ts.CallExpression | ts.NewExpression,
  type: ts.Type,
  index: number,
  thenableReturnIndices: Set<number>,
  voidReturnIndices: Set<number>,
): void {
  if (isThenableReturningFunctionType(checker, node.expression, type)) {
    thenableReturnIndices.add(index);
  } else if (
    isVoidReturningFunctionType(checker, node.expression, type) &&
    // If a certain argument accepts both thenable and void returns,
    // a promise-returning function is valid
    !thenableReturnIndices.has(index)
  ) {
    voidReturnIndices.add(index);
  }
  const contextualType = checker.getContextualTypeForArgumentAtIndex(
    node,
    index,
  );
  if (contextualType !== type) {
    checkThenableOrVoidArgument(
      checker,
      node,
      contextualType,
      index,
      thenableReturnIndices,
      voidReturnIndices,
    );
  }
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `node: ts.CallExpression | ts.NewExpression`
  - `type: ts.Type`
  - `index: number`
  - `thenableReturnIndices: Set<number>`
  - `voidReturnIndices: Set<number>`
- **Return Type**: `void`
- **Calls**:
  - `isThenableReturningFunctionType`
  - `thenableReturnIndices.add`
  - `isVoidReturningFunctionType`
  - `thenableReturnIndices.has`
  - `voidReturnIndices.add`
  - `checker.getContextualTypeForArgumentAtIndex`
  - `checkThenableOrVoidArgument`
- **Internal Comments**:
```
// If a certain argument accepts both thenable and void returns,
// a promise-returning function is valid
```

### `voidFunctionArguments(checker: ts.TypeChecker, node: ts.CallExpression | ts.NewExpression): Set<number>`

<details><summary>Code</summary>

```ts
function voidFunctionArguments(
  checker: ts.TypeChecker,
  node: ts.CallExpression | ts.NewExpression,
): Set<number> {
  // 'new' can be used without any arguments, as in 'let b = new Object;'
  // In this case, there are no argument positions to check, so return early.
  if (!node.arguments) {
    return new Set<number>();
  }
  const thenableReturnIndices = new Set<number>();
  const voidReturnIndices = new Set<number>();
  const type = checker.getTypeAtLocation(node.expression);

  // We can't use checker.getResolvedSignature because it prefers an early '() => void' over a later '() => Promise<void>'
  // See https://github.com/microsoft/TypeScript/issues/48077

  for (const subType of tsutils.unionConstituents(type)) {
    // Standard function calls and `new` have two different types of signatures
    const signatures = ts.isCallExpression(node)
      ? subType.getCallSignatures()
      : subType.getConstructSignatures();
    for (const signature of signatures) {
      for (const [index, parameter] of signature.parameters.entries()) {
        const decl = parameter.valueDeclaration;
        let type = checker.getTypeOfSymbolAtLocation(
          parameter,
          node.expression,
        );

        // If this is a array 'rest' parameter, check all of the argument indices
        // from the current argument to the end.
        if (decl && isRestParameterDeclaration(decl)) {
          if (checker.isArrayType(type)) {
            // Unwrap 'Array<MaybeVoidFunction>' to 'MaybeVoidFunction',
            // so that we'll handle it in the same way as a non-rest
            // 'param: MaybeVoidFunction'
            type = checker.getTypeArguments(type)[0];
            for (let i = index; i < node.arguments.length; i++) {
              checkThenableOrVoidArgument(
                checker,
                node,
                type,
                i,
                thenableReturnIndices,
                voidReturnIndices,
              );
            }
          } else if (checker.isTupleType(type)) {
            // Check each type in the tuple - for example, [boolean, () => void] would
            // add the index of the second tuple parameter to 'voidReturnIndices'
            const typeArgs = checker.getTypeArguments(type);
            for (
              let i = index;
              i < node.arguments.length && i - index < typeArgs.length;
              i++
            ) {
              checkThenableOrVoidArgument(
                checker,
                node,
                typeArgs[i - index],
                i,
                thenableReturnIndices,
                voidReturnIndices,
              );
            }
          }
        } else {
          checkThenableOrVoidArgument(
            checker,
            node,
            type,
            index,
            thenableReturnIndices,
            voidReturnIndices,
          );
        }
      }
    }
  }

  for (const index of thenableReturnIndices) {
    voidReturnIndices.delete(index);
  }

  return voidReturnIndices;
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `node: ts.CallExpression | ts.NewExpression`
- **Return Type**: `Set<number>`
- **Calls**:
  - `checker.getTypeAtLocation`
  - `tsutils.unionConstituents`
  - `ts.isCallExpression`
  - `subType.getCallSignatures`
  - `subType.getConstructSignatures`
  - `signature.parameters.entries`
  - `checker.getTypeOfSymbolAtLocation`
  - `isRestParameterDeclaration (from ../util)`
  - `checker.isArrayType`
  - `checker.getTypeArguments`
  - `checkThenableOrVoidArgument`
  - `checker.isTupleType`
  - `voidReturnIndices.delete`
- **Internal Comments**:
```
// 'new' can be used without any arguments, as in 'let b = new Object;'
// In this case, there are no argument positions to check, so return early.
// We can't use checker.getResolvedSignature because it prefers an early '() => void' over a later '() => Promise<void>'
// See https://github.com/microsoft/TypeScript/issues/48077
// Standard function calls and `new` have two different types of signatures (x2)
// If this is a array 'rest' parameter, check all of the argument indices
// from the current argument to the end.
// Unwrap 'Array<MaybeVoidFunction>' to 'MaybeVoidFunction', (x3)
// so that we'll handle it in the same way as a non-rest (x3)
// 'param: MaybeVoidFunction' (x3)
// Check each type in the tuple - for example, [boolean, () => void] would (x2)
// add the index of the second tuple parameter to 'voidReturnIndices' (x2)
```

### `anySignatureIsThenableType(checker: ts.TypeChecker, node: ts.Node, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function anySignatureIsThenableType(
  checker: ts.TypeChecker,
  node: ts.Node,
  type: ts.Type,
): boolean {
  for (const signature of type.getCallSignatures()) {
    const returnType = signature.getReturnType();
    if (tsutils.isThenableType(checker, node, returnType)) {
      return true;
    }
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns Whether any call signature of the type has a thenable return type.
 */
```

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `node: ts.Node`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `type.getCallSignatures`
  - `signature.getReturnType`
  - `tsutils.isThenableType`
### `isThenableReturningFunctionType(checker: ts.TypeChecker, node: ts.Node, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isThenableReturningFunctionType(
  checker: ts.TypeChecker,
  node: ts.Node,
  type: ts.Type,
): boolean {
  for (const subType of tsutils.unionConstituents(type)) {
    if (anySignatureIsThenableType(checker, node, subType)) {
      return true;
    }
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns Whether type is a thenable-returning function.
 */
```

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `node: ts.Node`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.unionConstituents`
  - `anySignatureIsThenableType`
### `isVoidReturningFunctionType(checker: ts.TypeChecker, node: ts.Node, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isVoidReturningFunctionType(
  checker: ts.TypeChecker,
  node: ts.Node,
  type: ts.Type,
): boolean {
  let hadVoidReturn = false;

  for (const subType of tsutils.unionConstituents(type)) {
    for (const signature of subType.getCallSignatures()) {
      const returnType = signature.getReturnType();

      // If a certain positional argument accepts both thenable and void returns,
      // a promise-returning function is valid
      if (tsutils.isThenableType(checker, node, returnType)) {
        return false;
      }

      hadVoidReturn ||= tsutils.isTypeFlagSet(returnType, ts.TypeFlags.Void);
    }
  }

  return hadVoidReturn;
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns Whether type is a void-returning function.
 */
```

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `node: ts.Node`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.unionConstituents`
  - `subType.getCallSignatures`
  - `signature.getReturnType`
  - `tsutils.isThenableType`
  - `tsutils.isTypeFlagSet`
- **Internal Comments**:
```
// If a certain positional argument accepts both thenable and void returns,
// a promise-returning function is valid
```

### `returnsThenable(checker: ts.TypeChecker, node: ts.Node): boolean`

<details><summary>Code</summary>

```ts
function returnsThenable(checker: ts.TypeChecker, node: ts.Node): boolean {
  const type = checker.getApparentType(checker.getTypeAtLocation(node));
  return tsutils
    .unionConstituents(type)
    .some(t => anySignatureIsThenableType(checker, node, t));
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns Whether expression is a function that returns a thenable.
 */
```

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `node: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `checker.getApparentType`
  - `checker.getTypeAtLocation`
  - `tsutils
    .unionConstituents(type)
    .some`
  - `anySignatureIsThenableType`
### `getHeritageTypes(checker: ts.TypeChecker, tsNode: ts.ClassDeclaration | ts.ClassExpression | ts.InterfaceDeclaration): ts.Type[] | undefined`

<details><summary>Code</summary>

```ts
function getHeritageTypes(
  checker: ts.TypeChecker,
  tsNode: ts.ClassDeclaration | ts.ClassExpression | ts.InterfaceDeclaration,
): ts.Type[] | undefined {
  return tsNode.heritageClauses
    ?.flatMap(clause => clause.types)
    .map(typeExpression => checker.getTypeAtLocation(typeExpression));
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `tsNode: ts.ClassDeclaration | ts.ClassExpression | ts.InterfaceDeclaration`
- **Return Type**: `ts.Type[] | undefined`
- **Calls**:
  - `tsNode.heritageClauses
    ?.flatMap(clause => clause.types)
    .map`
  - `checker.getTypeAtLocation`
### `getMemberIfExists(type: ts.Type, memberName: string): ts.Symbol | undefined`

<details><summary>Code</summary>

```ts
function getMemberIfExists(
  type: ts.Type,
  memberName: string,
): ts.Symbol | undefined {
  const escapedMemberName = ts.escapeLeadingUnderscores(memberName);
  const symbolMemberMatch = type.getSymbol()?.members?.get(escapedMemberName);
  return (
    symbolMemberMatch ?? tsutils.getPropertyOfType(type, escapedMemberName)
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns The member with the given name in `type`, if it exists.
 */
```

- **Parameters**:
  - `type: ts.Type`
  - `memberName: string`
- **Return Type**: `ts.Symbol | undefined`
- **Calls**:
  - `ts.escapeLeadingUnderscores`
  - `type.getSymbol()?.members?.get`
  - `tsutils.getPropertyOfType`
### `isStaticMember(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isStaticMember(node: TSESTree.Node): boolean {
  return (
    (node.type === AST_NODE_TYPES.MethodDefinition ||
      node.type === AST_NODE_TYPES.PropertyDefinition ||
      node.type === AST_NODE_TYPES.AccessorProperty) &&
    node.static
  );
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`

---

## Interfaces

### `ChecksVoidReturnOptions`

<details><summary>Interface Code</summary>

```ts
export interface ChecksVoidReturnOptions {
  arguments?: boolean;
  attributes?: boolean;
  inheritedMethods?: boolean;
  properties?: boolean;
  returns?: boolean;
  variables?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `arguments` | `boolean` | ✓ |  |
| `attributes` | `boolean` | ✓ |  |
| `inheritedMethods` | `boolean` | ✓ |  |
| `properties` | `boolean` | ✓ |  |
| `returns` | `boolean` | ✓ |  |
| `variables` | `boolean` | ✓ |  |


---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    checksConditionals?: boolean;
    checksSpreads?: boolean;
    checksVoidReturn?: boolean | ChecksVoidReturnOptions;
  },
];
```

### `MessageId`

```ts
type MessageId = | 'conditional'
  | 'predicate'
  | 'spread'
  | 'voidReturnArgument'
  | 'voidReturnAttribute'
  | 'voidReturnInheritedMethod'
  | 'voidReturnProperty'
  | 'voidReturnReturnValue'
  | 'voidReturnVariable';
```


---