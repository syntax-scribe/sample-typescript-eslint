[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unsafe-return.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 14 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unsafe-return.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AnyType` | `../util` |
| `createRule` | `../util` |
| `discriminateAnyType` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getContextualType` | `../util` |
| `getParserServices` | `../util` |
| `getThisExpression` | `../util` |
| `isTypeAnyType` | `../util` |
| `isTypeFlagSet` | `../util` |
| `isTypeUnknownArrayType` | `../util` |
| `isTypeUnknownType` | `../util` |
| `isUnsafeAssignment` | `../util` |
| `getParentFunctionNode` | `../util/getParentFunctionNode` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `functionType` | `any` | let/var | `ts.isFunctionExpression(functionTSNode) ||
        ts.isArrowFunction(functionTSNode)
          ? getContextualType(checker, functionTSNode)
          : services.getTypeAtLocation(functionNode)` | ✗ |
| `messageId` | `'unsafeReturn' | 'unsafeReturnThis'` | let/var | `'unsafeReturn'` | ✗ |
| `argument` | `any` | const | `node.argument` | ✗ |


---

## Functions

### `checkReturn(returnNode: TSESTree.Node, reportingNode: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
function checkReturn(
      returnNode: TSESTree.Node,
      reportingNode: TSESTree.Node = returnNode,
    ): void {
      const tsNode = services.esTreeNodeToTSNodeMap.get(returnNode);
      const type = checker.getTypeAtLocation(tsNode);

      const anyType = discriminateAnyType(
        type,
        checker,
        services.program,
        tsNode,
      );
      const functionNode = getParentFunctionNode(returnNode);
      /* istanbul ignore if */ if (!functionNode) {
        return;
      }

      // function has an explicit return type, so ensure it's a safe return
      const returnNodeType = getConstrainedTypeAtLocation(services, returnNode);
      const functionTSNode = services.esTreeNodeToTSNodeMap.get(functionNode);

      // function expressions will not have their return type modified based on receiver typing
      // so we have to use the contextual typing in these cases, i.e.
      // const foo1: () => Set<string> = () => new Set<any>();
      // the return type of the arrow function is Set<any> even though the variable is typed as Set<string>
      let functionType =
        ts.isFunctionExpression(functionTSNode) ||
        ts.isArrowFunction(functionTSNode)
          ? getContextualType(checker, functionTSNode)
          : services.getTypeAtLocation(functionNode);
      functionType ??= services.getTypeAtLocation(functionNode);
      const callSignatures = tsutils.getCallSignaturesOfType(functionType);
      // If there is an explicit type annotation *and* that type matches the actual
      // function return type, we shouldn't complain (it's intentional, even if unsafe)
      if (functionTSNode.type) {
        for (const signature of callSignatures) {
          const signatureReturnType = signature.getReturnType();

          if (
            returnNodeType === signatureReturnType ||
            isTypeFlagSet(
              signatureReturnType,
              ts.TypeFlags.Any | ts.TypeFlags.Unknown,
            )
          ) {
            return;
          }
          if (functionNode.async) {
            const awaitedSignatureReturnType =
              checker.getAwaitedType(signatureReturnType);

            const awaitedReturnNodeType =
              checker.getAwaitedType(returnNodeType);
            if (
              awaitedReturnNodeType === awaitedSignatureReturnType ||
              (awaitedSignatureReturnType &&
                isTypeFlagSet(
                  awaitedSignatureReturnType,
                  ts.TypeFlags.Any | ts.TypeFlags.Unknown,
                ))
            ) {
              return;
            }
          }
        }
      }

      if (anyType !== AnyType.Safe) {
        // Allow cases when the declared return type of the function is either unknown or unknown[]
        // and the function is returning any or any[].
        for (const signature of callSignatures) {
          const functionReturnType = signature.getReturnType();
          if (
            anyType === AnyType.Any &&
            isTypeUnknownType(functionReturnType)
          ) {
            return;
          }
          if (
            anyType === AnyType.AnyArray &&
            isTypeUnknownArrayType(functionReturnType, checker)
          ) {
            return;
          }
          const awaitedType = checker.getAwaitedType(functionReturnType);
          if (
            awaitedType &&
            anyType === AnyType.PromiseAny &&
            isTypeUnknownType(awaitedType)
          ) {
            return;
          }
        }

        if (anyType === AnyType.PromiseAny && !functionNode.async) {
          return;
        }

        let messageId: 'unsafeReturn' | 'unsafeReturnThis' = 'unsafeReturn';
        const isErrorType = tsutils.isIntrinsicErrorType(returnNodeType);

        if (!isNoImplicitThis) {
          // `return this`
          const thisExpression = getThisExpression(returnNode);
          if (
            thisExpression &&
            isTypeAnyType(
              getConstrainedTypeAtLocation(services, thisExpression),
            )
          ) {
            messageId = 'unsafeReturnThis';
          }
        }

        // If the function return type was not unknown/unknown[], mark usage as unsafeReturn.
        return context.report({
          node: reportingNode,
          messageId,
          data: {
            type: isErrorType
              ? 'error'
              : anyType === AnyType.Any
                ? '`any`'
                : anyType === AnyType.PromiseAny
                  ? '`Promise<any>`'
                  : '`any[]`',
          },
        });
      }

      const signature = functionType.getCallSignatures().at(0);
      if (signature) {
        const functionReturnType = signature.getReturnType();
        const result = isUnsafeAssignment(
          returnNodeType,
          functionReturnType,
          checker,
          returnNode,
        );
        if (!result) {
          return;
        }

        const { receiver, sender } = result;
        return context.report({
          node: reportingNode,
          messageId: 'unsafeReturnAssignment',
          data: {
            receiver: checker.typeToString(receiver),
            sender: checker.typeToString(sender),
          },
        });
      }
    }
```
</details>

- **Parameters**:
  - `returnNode: TSESTree.Node`
  - `reportingNode: TSESTree.Node`
- **Return Type**: `void`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `checker.getTypeAtLocation`
  - `discriminateAnyType (from ../util)`
  - `getParentFunctionNode (from ../util/getParentFunctionNode)`
  - `getConstrainedTypeAtLocation (from ../util)`
  - `ts.isFunctionExpression`
  - `ts.isArrowFunction`
  - `getContextualType (from ../util)`
  - `services.getTypeAtLocation`
  - `tsutils.getCallSignaturesOfType`
  - `signature.getReturnType`
  - `isTypeFlagSet (from ../util)`
  - `checker.getAwaitedType`
  - `isTypeUnknownType (from ../util)`
  - `isTypeUnknownArrayType (from ../util)`
  - `tsutils.isIntrinsicErrorType`
  - `getThisExpression (from ../util)`
  - `isTypeAnyType (from ../util)`
  - `context.report`
  - `functionType.getCallSignatures().at`
  - `isUnsafeAssignment (from ../util)`
  - `checker.typeToString`
- **Internal Comments**:
```
/* istanbul ignore if */
// function has an explicit return type, so ensure it's a safe return (x2)
// function expressions will not have their return type modified based on receiver typing (x2)
// so we have to use the contextual typing in these cases, i.e. (x2)
// const foo1: () => Set<string> = () => new Set<any>(); (x2)
// the return type of the arrow function is Set<any> even though the variable is typed as Set<string> (x2)
// If there is an explicit type annotation *and* that type matches the actual
// function return type, we shouldn't complain (it's intentional, even if unsafe)
// Allow cases when the declared return type of the function is either unknown or unknown[]
// and the function is returning any or any[].
// `return this` (x2)
// If the function return type was not unknown/unknown[], mark usage as unsafeReturn.
```


---