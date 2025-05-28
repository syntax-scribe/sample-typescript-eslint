[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `only-throw-error.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 15 |
| 📊 Variables & Constants | 5 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/only-throw-error.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `isThenableType` | `ts-api-utils` |
| `TypeOrValueSpecifier` | `../util` |
| `createRule` | `../util` |
| `findVariable` | `../util` |
| `getParserServices` | `../util` |
| `isErrorLike` | `../util` |
| `isTypeAnyType` | `../util` |
| `isTypeUnknownType` | `../util` |
| `typeMatchesSomeSpecifier` | `../util` |
| `typeOrValueSpecifiersSchema` | `../util` |
| `nullThrows` | `../util` |
| `parseCatchCall` | `../util/promiseUtils` |
| `parseThenCall` | `../util/promiseUtils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `allow` | `any` | const | `options.allow` | ✗ |
| `def` | `any` | const | `smVariable.defs[0]` | ✗ |
| `callExpression` | `any` | const | `def.node.parent` | ✗ |
| `parsedPromiseHandlingCall` | `{ onRejected?: any; object: TSESTree.Expression; }` | const | `parseCatchCall(callExpression, context) ??
          parseThenCall(callExpression, context)` | ✗ |
| `tsObjectNode` | `ts.Expression` | const | `services.esTreeNodeToTSNodeMap.get(
              object,
            ) as ts.Expression` | ✗ |


---

## Functions

### `isRethrownError(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isRethrownError(node: TSESTree.Node): boolean {
      if (node.type !== AST_NODE_TYPES.Identifier) {
        return false;
      }

      const scope = context.sourceCode.getScope(node);

      const smVariable = nullThrows(
        findVariable(scope, node),
        `Variable ${node.name} should exist in scope manager`,
      );

      const variableDefinitions = smVariable.defs.filter(
        def => def.isVariableDefinition,
      );
      if (variableDefinitions.length !== 1) {
        return false;
      }
      const def = smVariable.defs[0];

      // try { /* ... */ } catch (x) { throw x; }
      if (def.node.type === AST_NODE_TYPES.CatchClause) {
        return true;
      }

      // promise.catch(x => { throw x; })
      // promise.then(onFulfilled, x => { throw x; })
      if (
        def.node.type === AST_NODE_TYPES.ArrowFunctionExpression &&
        def.node.params.length >= 1 &&
        def.node.params[0] === def.name &&
        def.node.parent.type === AST_NODE_TYPES.CallExpression
      ) {
        const callExpression = def.node.parent;

        const parsedPromiseHandlingCall =
          parseCatchCall(callExpression, context) ??
          parseThenCall(callExpression, context);
        if (parsedPromiseHandlingCall != null) {
          const { object, onRejected } = parsedPromiseHandlingCall;
          if (onRejected === def.node) {
            const tsObjectNode = services.esTreeNodeToTSNodeMap.get(
              object,
            ) as ts.Expression;

            // make sure we're actually dealing with a promise
            if (
              isThenableType(services.program.getTypeChecker(), tsObjectNode)
            ) {
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
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode.getScope`
  - `nullThrows (from ../util)`
  - `findVariable (from ../util)`
  - `smVariable.defs.filter`
  - `parseCatchCall (from ../util/promiseUtils)`
  - `parseThenCall (from ../util/promiseUtils)`
  - `services.esTreeNodeToTSNodeMap.get`
  - `isThenableType (from ts-api-utils)`
  - `services.program.getTypeChecker`
- **Internal Comments**:
```
// try { /* ... */ } catch (x) { throw x; }
// promise.catch(x => { throw x; })
// promise.then(onFulfilled, x => { throw x; })
// make sure we're actually dealing with a promise
```

### `checkThrowArgument(node: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
function checkThrowArgument(node: TSESTree.Node): void {
      if (
        node.type === AST_NODE_TYPES.AwaitExpression ||
        node.type === AST_NODE_TYPES.YieldExpression
      ) {
        return;
      }

      if (options.allowRethrowing && isRethrownError(node)) {
        return;
      }

      const type = services.getTypeAtLocation(node);

      if (typeMatchesSomeSpecifier(type, allow, services.program)) {
        return;
      }

      if (type.flags & ts.TypeFlags.Undefined) {
        context.report({ node, messageId: 'undef' });
        return;
      }

      if (options.allowThrowingAny && isTypeAnyType(type)) {
        return;
      }

      if (options.allowThrowingUnknown && isTypeUnknownType(type)) {
        return;
      }

      if (isErrorLike(services.program, type)) {
        return;
      }

      context.report({ node, messageId: 'object' });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `void`
- **Calls**:
  - `isRethrownError`
  - `services.getTypeAtLocation`
  - `typeMatchesSomeSpecifier (from ../util)`
  - `context.report`
  - `isTypeAnyType (from ../util)`
  - `isTypeUnknownType (from ../util)`
  - `isErrorLike (from ../util)`

---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = 'object' | 'undef';
```

### `Options`

```ts
type Options = [
  {
    allow?: TypeOrValueSpecifier[];
    allowRethrowing?: boolean;
    allowThrowingAny?: boolean;
    allowThrowingUnknown?: boolean;
  },
];
```


---