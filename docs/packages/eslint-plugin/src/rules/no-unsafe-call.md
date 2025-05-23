[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unsafe-call.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unsafe-call.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `getThisExpression` | `../util` |
| `isBuiltinSymbolLike` | `../util` |
| `isTypeAnyType` | `../util` |


---

## Functions

### `checkCall(node: TSESTree.Node, reportingNode: TSESTree.Node, messageId: MessageIds): void`

<details><summary>Code</summary>

```ts
function checkCall(
      node: TSESTree.Node,
      reportingNode: TSESTree.Node,
      messageId: MessageIds,
    ): void {
      const type = getConstrainedTypeAtLocation(services, node);

      if (isTypeAnyType(type)) {
        if (!isNoImplicitThis) {
          // `this()` or `this.foo()` or `this.foo[bar]()`
          const thisExpression = getThisExpression(node);
          if (
            thisExpression &&
            isTypeAnyType(
              getConstrainedTypeAtLocation(services, thisExpression),
            )
          ) {
            messageId = 'unsafeCallThis';
          }
        }

        const isErrorType = tsutils.isIntrinsicErrorType(type);

        context.report({
          node: reportingNode,
          messageId,
          data: {
            type: isErrorType ? '`error` type' : '`any`',
          },
        });
        return;
      }

      if (isBuiltinSymbolLike(services.program, type, 'Function')) {
        // this also matches subtypes of `Function`, like `interface Foo extends Function {}`.
        //
        // For weird TS reasons that I don't understand, these are
        //
        // safe to construct if:
        // - they have at least one call signature _that is not void-returning_,
        // - OR they have at least one construct signature.
        //
        // safe to call (including as template) if:
        // - they have at least one call signature
        // - OR they have at least one construct signature.

        const constructSignatures = type.getConstructSignatures();
        if (constructSignatures.length > 0) {
          return;
        }

        const callSignatures = type.getCallSignatures();
        if (messageId === 'unsafeNew') {
          if (
            callSignatures.some(
              signature =>
                !tsutils.isIntrinsicVoidType(signature.getReturnType()),
            )
          ) {
            return;
          }
        } else if (callSignatures.length > 0) {
          return;
        }

        context.report({
          node: reportingNode,
          messageId,
          data: {
            type: '`Function`',
          },
        });
        return;
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `reportingNode: TSESTree.Node`
  - `messageId: MessageIds`
- **Return Type**: `void`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `isTypeAnyType (from ../util)`
  - `getThisExpression (from ../util)`
  - `tsutils.isIntrinsicErrorType`
  - `context.report`
  - `isBuiltinSymbolLike (from ../util)`
  - `type.getConstructSignatures`
  - `type.getCallSignatures`
  - `callSignatures.some`
  - `tsutils.isIntrinsicVoidType`
  - `signature.getReturnType`
- **Internal Comments**:
```
// `this()` or `this.foo()` or `this.foo[bar]()` (x2)
// this also matches subtypes of `Function`, like `interface Foo extends Function {}`. (x2)
// (x6)
// For weird TS reasons that I don't understand, these are (x2)
// safe to construct if: (x2)
// - they have at least one call signature _that is not void-returning_, (x2)
// - OR they have at least one construct signature. (x4)
// safe to call (including as template) if: (x2)
// - they have at least one call signature (x2)
```


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = | 'unsafeCall'
  | 'unsafeCallThis'
  | 'unsafeNew'
  | 'unsafeTemplateTag';
```


---