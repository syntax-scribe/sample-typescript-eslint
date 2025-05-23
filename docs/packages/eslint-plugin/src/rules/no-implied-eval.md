[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-implied-eval.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 5
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-implied-eval.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `isBuiltinSymbolLike` | `../util` |
| `isReferenceToGlobalFunction` | `../util` |


---

## Functions

### `getCalleeName(node: TSESTree.Expression): string | null`

<details><summary>Code</summary>

```ts
function getCalleeName(node: TSESTree.Expression): string | null {
      if (node.type === AST_NODE_TYPES.Identifier) {
        return node.name;
      }

      if (
        node.type === AST_NODE_TYPES.MemberExpression &&
        node.object.type === AST_NODE_TYPES.Identifier &&
        GLOBAL_CANDIDATES.has(node.object.name)
      ) {
        if (node.property.type === AST_NODE_TYPES.Identifier) {
          return node.property.name;
        }

        if (
          node.property.type === AST_NODE_TYPES.Literal &&
          typeof node.property.value === 'string'
        ) {
          return node.property.value;
        }
      }

      return null;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `string | null`
- **Calls**:
  - `GLOBAL_CANDIDATES.has`
### `isFunctionType(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isFunctionType(node: TSESTree.Node): boolean {
      const type = services.getTypeAtLocation(node);
      const symbol = type.getSymbol();

      if (
        symbol &&
        tsutils.isSymbolFlagSet(
          symbol,
          ts.SymbolFlags.Function | ts.SymbolFlags.Method,
        )
      ) {
        return true;
      }

      if (isBuiltinSymbolLike(services.program, type, FUNCTION_CONSTRUCTOR)) {
        return true;
      }

      const signatures = checker.getSignaturesOfType(
        type,
        ts.SignatureKind.Call,
      );

      return signatures.length > 0;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `services.getTypeAtLocation`
  - `type.getSymbol`
  - `tsutils.isSymbolFlagSet`
  - `isBuiltinSymbolLike (from ../util)`
  - `checker.getSignaturesOfType`
### `isBind(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isBind(node: TSESTree.Node): boolean {
      return node.type === AST_NODE_TYPES.MemberExpression
        ? isBind(node.property)
        : node.type === AST_NODE_TYPES.Identifier && node.name === 'bind';
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isBind`
### `isFunction(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isFunction(node: TSESTree.Node): boolean {
      switch (node.type) {
        case AST_NODE_TYPES.ArrowFunctionExpression:
        case AST_NODE_TYPES.FunctionDeclaration:
        case AST_NODE_TYPES.FunctionExpression:
          return true;

        case AST_NODE_TYPES.Literal:
        case AST_NODE_TYPES.TemplateLiteral:
          return false;

        case AST_NODE_TYPES.CallExpression:
          return isBind(node.callee) || isFunctionType(node);

        default:
          return isFunctionType(node);
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isBind`
  - `isFunctionType`
### `checkImpliedEval(node: TSESTree.CallExpression | TSESTree.NewExpression): void`

<details><summary>Code</summary>

```ts
function checkImpliedEval(
      node: TSESTree.CallExpression | TSESTree.NewExpression,
    ): void {
      const calleeName = getCalleeName(node.callee);
      if (calleeName == null) {
        return;
      }

      if (calleeName === FUNCTION_CONSTRUCTOR) {
        const type = services.getTypeAtLocation(node.callee);
        const symbol = type.getSymbol();
        if (symbol) {
          if (
            isBuiltinSymbolLike(services.program, type, 'FunctionConstructor')
          ) {
            context.report({ node, messageId: 'noFunctionConstructor' });
            return;
          }
        } else {
          context.report({ node, messageId: 'noFunctionConstructor' });
          return;
        }
      }

      if (node.arguments.length === 0) {
        return;
      }

      const [handler] = node.arguments;
      if (
        EVAL_LIKE_FUNCTIONS.has(calleeName) &&
        !isFunction(handler) &&
        isReferenceToGlobalFunction(calleeName, node, context.sourceCode)
      ) {
        context.report({ node: handler, messageId: 'noImpliedEvalError' });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression | TSESTree.NewExpression`
- **Return Type**: `void`
- **Calls**:
  - `getCalleeName`
  - `services.getTypeAtLocation`
  - `type.getSymbol`
  - `isBuiltinSymbolLike (from ../util)`
  - `context.report`
  - `EVAL_LIKE_FUNCTIONS.has`
  - `isFunction`
  - `isReferenceToGlobalFunction (from ../util)`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---