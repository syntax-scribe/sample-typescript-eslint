[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-promise-reject-errors.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 14 |
| 📊 Variables & Constants | 1 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-promise-reject-errors.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `isErrorLike` | `../util` |
| `isTypeAnyType` | `../util` |
| `isTypeUnknownType` | `../util` |
| `isFunction` | `../util` |
| `isIdentifier` | `../util` |
| `isPromiseConstructorLike` | `../util` |
| `isPromiseLike` | `../util` |
| `isReadonlyErrorLike` | `../util` |
| `isStaticMemberAccessOfValue` | `../util` |
| `skipChainExpression` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `rejectVariable` | `any` | const | `context.sourceCode
          .getDeclaredVariables(executor)
          .find(variable => variable.identifiers.includes(rejectParamNode))!` | ✗ |


---

## Functions

### `checkRejectCall(callExpression: TSESTree.CallExpression): void`

<details><summary>Code</summary>

```ts
function checkRejectCall(callExpression: TSESTree.CallExpression): void {
      const argument = callExpression.arguments.at(0);
      if (argument) {
        const type = services.getTypeAtLocation(argument);

        if (options.allowThrowingAny && isTypeAnyType(type)) {
          return;
        }

        if (options.allowThrowingUnknown && isTypeUnknownType(type)) {
          return;
        }

        if (
          isErrorLike(services.program, type) ||
          isReadonlyErrorLike(services.program, type)
        ) {
          return;
        }
      } else if (options.allowEmptyReject) {
        return;
      }

      context.report({
        node: callExpression,
        messageId: 'rejectAnError',
      });
    }
```
</details>

- **Parameters**:
  - `callExpression: TSESTree.CallExpression`
- **Return Type**: `void`
- **Calls**:
  - `callExpression.arguments.at`
  - `services.getTypeAtLocation`
  - `isTypeAnyType (from ../util)`
  - `isTypeUnknownType (from ../util)`
  - `isErrorLike (from ../util)`
  - `isReadonlyErrorLike (from ../util)`
  - `context.report`
### `typeAtLocationIsLikePromise(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function typeAtLocationIsLikePromise(node: TSESTree.Node): boolean {
      const type = services.getTypeAtLocation(node);
      return (
        isPromiseConstructorLike(services.program, type) ||
        isPromiseLike(services.program, type)
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `services.getTypeAtLocation`
  - `isPromiseConstructorLike (from ../util)`
  - `isPromiseLike (from ../util)`

---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = 'rejectAnError';
```

### `Options`

```ts
type Options = [
  {
    allowEmptyReject?: boolean;
    allowThrowingAny?: boolean;
    allowThrowingUnknown?: boolean;
  },
];
```


---