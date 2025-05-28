[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `promise-function-async.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |
| 🧱 Classes | 0 |
| 📦 Imports | 10 |
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
📂 **`packages/eslint-plugin/src/rules/promise-function-async.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `containsAllTypesByName` | `../util` |
| `createRule` | `../util` |
| `getFunctionHeadLoc` | `../util` |
| `getParserServices` | `../util` |
| `isTypeFlagSet` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `allAllowedPromiseNames` | `Set<any>` | const | `new Set([
      'Promise',
      // https://github.com/typescript-eslint/typescript-eslint/issues/5439
      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      ...allowedPromiseNames!,
    ])` | ✗ |
| `method` | `any` | const | `node.parent` | ✗ |
| `lastDecorator` | `any` | const | `method.decorators[method.decorators.length - 1]` | ✗ |
| `insertSpace` | `boolean` | const | `!context.sourceCode.isSpaceBetween(
                nullThrows(
                  context.sourceCode.getTokenBefore(keyToken),
                  NullThrowsReasons.MissingToken('token', 'keyword'),
                ),
                keyToken,
              )` | ✗ |
| `code` | `string` | let/var | `'async '` | ✗ |


---

## Functions

### `validateNode(node: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression): void`

<details><summary>Code</summary>

```ts
function validateNode(
      node:
        | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression,
    ): void {
      if (node.parent.type === AST_NODE_TYPES.TSAbstractMethodDefinition) {
        // Abstract method can't be async
        return;
      }

      if (
        (node.parent.type === AST_NODE_TYPES.Property ||
          node.parent.type === AST_NODE_TYPES.MethodDefinition) &&
        (node.parent.kind === 'get' || node.parent.kind === 'set')
      ) {
        // Getters and setters can't be async
        return;
      }

      const signatures = services.getTypeAtLocation(node).getCallSignatures();
      if (!signatures.length) {
        return;
      }

      const returnTypes = signatures.map(signature =>
        checker.getReturnTypeOfSignature(signature),
      );

      if (
        !allowAny &&
        returnTypes.some(type =>
          isTypeFlagSet(type, ts.TypeFlags.Any | ts.TypeFlags.Unknown),
        )
      ) {
        // Report without auto fixer because the return type is unknown
        return context.report({
          loc: getFunctionHeadLoc(node, context.sourceCode),
          node,
          messageId: 'missingAsync',
        });
      }

      if (
        // require all potential return types to be promise/any/unknown
        returnTypes.every(type =>
          containsAllTypesByName(
            type,
            true,
            allAllowedPromiseNames,
            // If no return type is explicitly set, we check if any parts of the return type match a Promise (instead of requiring all to match).
            node.returnType == null,
          ),
        )
      ) {
        const isHybridReturnType = returnTypes.some(
          type =>
            type.isUnion() &&
            !type.types.every(part =>
              containsAllTypesByName(part, true, allAllowedPromiseNames),
            ),
        );

        context.report({
          loc: getFunctionHeadLoc(node, context.sourceCode),
          node,
          messageId: isHybridReturnType
            ? 'missingAsyncHybridReturn'
            : 'missingAsync',
          fix: fixer => {
            if (
              node.parent.type === AST_NODE_TYPES.MethodDefinition ||
              (node.parent.type === AST_NODE_TYPES.Property &&
                node.parent.method)
            ) {
              // this function is a class method or object function property shorthand
              const method = node.parent;

              // the token to put `async` before
              let keyToken = nullThrows(
                context.sourceCode.getFirstToken(method),
                NullThrowsReasons.MissingToken('key token', 'method'),
              );

              // if there are decorators then skip past them
              if (
                method.type === AST_NODE_TYPES.MethodDefinition &&
                method.decorators.length
              ) {
                const lastDecorator =
                  method.decorators[method.decorators.length - 1];
                keyToken = nullThrows(
                  context.sourceCode.getTokenAfter(lastDecorator),
                  NullThrowsReasons.MissingToken('key token', 'last decorator'),
                );
              }

              // if current token is a keyword like `static` or `public` then skip it
              while (
                keyToken.type === AST_TOKEN_TYPES.Keyword &&
                keyToken.range[0] < method.key.range[0]
              ) {
                keyToken = nullThrows(
                  context.sourceCode.getTokenAfter(keyToken),
                  NullThrowsReasons.MissingToken('token', 'keyword'),
                );
              }

              // check if there is a space between key and previous token
              const insertSpace = !context.sourceCode.isSpaceBetween(
                nullThrows(
                  context.sourceCode.getTokenBefore(keyToken),
                  NullThrowsReasons.MissingToken('token', 'keyword'),
                ),
                keyToken,
              );

              let code = 'async ';
              if (insertSpace) {
                code = ` ${code}`;
              }
              return fixer.insertTextBefore(keyToken, code);
            }

            return fixer.insertTextBefore(node, 'async ');
          },
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression`
- **Return Type**: `void`
- **Calls**:
  - `services.getTypeAtLocation(node).getCallSignatures`
  - `signatures.map`
  - `checker.getReturnTypeOfSignature`
  - `returnTypes.some`
  - `isTypeFlagSet (from ../util)`
  - `context.report`
  - `getFunctionHeadLoc (from ../util)`
  - `returnTypes.every`
  - `containsAllTypesByName (from ../util)`
  - `type.isUnion`
  - `type.types.every`
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `context.sourceCode.getTokenAfter`
  - `context.sourceCode.isSpaceBetween`
  - `context.sourceCode.getTokenBefore`
  - `fixer.insertTextBefore`
- **Internal Comments**:
```
// Abstract method can't be async
// Getters and setters can't be async
// Report without auto fixer because the return type is unknown
// require all potential return types to be promise/any/unknown (x3)
// If no return type is explicitly set, we check if any parts of the return type match a Promise (instead of requiring all to match). (x3)
// this function is a class method or object function property shorthand (x2)
// the token to put `async` before (x2)
// if there are decorators then skip past them
// if current token is a keyword like `static` or `public` then skip it
// check if there is a space between key and previous token (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
            if (
              node.parent.type === AST_NODE_TYPES.MethodDefinition ||
              (node.parent.type === AST_NODE_TYPES.Property &&
                node.parent.method)
            ) {
              // this function is a class method or object function property shorthand
              const method = node.parent;

              // the token to put `async` before
              let keyToken = nullThrows(
                context.sourceCode.getFirstToken(method),
                NullThrowsReasons.MissingToken('key token', 'method'),
              );

              // if there are decorators then skip past them
              if (
                method.type === AST_NODE_TYPES.MethodDefinition &&
                method.decorators.length
              ) {
                const lastDecorator =
                  method.decorators[method.decorators.length - 1];
                keyToken = nullThrows(
                  context.sourceCode.getTokenAfter(lastDecorator),
                  NullThrowsReasons.MissingToken('key token', 'last decorator'),
                );
              }

              // if current token is a keyword like `static` or `public` then skip it
              while (
                keyToken.type === AST_TOKEN_TYPES.Keyword &&
                keyToken.range[0] < method.key.range[0]
              ) {
                keyToken = nullThrows(
                  context.sourceCode.getTokenAfter(keyToken),
                  NullThrowsReasons.MissingToken('token', 'keyword'),
                );
              }

              // check if there is a space between key and previous token
              const insertSpace = !context.sourceCode.isSpaceBetween(
                nullThrows(
                  context.sourceCode.getTokenBefore(keyToken),
                  NullThrowsReasons.MissingToken('token', 'keyword'),
                ),
                keyToken,
              );

              let code = 'async ';
              if (insertSpace) {
                code = ` ${code}`;
              }
              return fixer.insertTextBefore(keyToken, code);
            }

            return fixer.insertTextBefore(node, 'async ');
          }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `context.sourceCode.getTokenAfter`
  - `context.sourceCode.isSpaceBetween`
  - `context.sourceCode.getTokenBefore`
  - `fixer.insertTextBefore`
- **Internal Comments**:
```
// this function is a class method or object function property shorthand (x2)
// the token to put `async` before (x2)
// if there are decorators then skip past them
// if current token is a keyword like `static` or `public` then skip it
// check if there is a space between key and previous token (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
            if (
              node.parent.type === AST_NODE_TYPES.MethodDefinition ||
              (node.parent.type === AST_NODE_TYPES.Property &&
                node.parent.method)
            ) {
              // this function is a class method or object function property shorthand
              const method = node.parent;

              // the token to put `async` before
              let keyToken = nullThrows(
                context.sourceCode.getFirstToken(method),
                NullThrowsReasons.MissingToken('key token', 'method'),
              );

              // if there are decorators then skip past them
              if (
                method.type === AST_NODE_TYPES.MethodDefinition &&
                method.decorators.length
              ) {
                const lastDecorator =
                  method.decorators[method.decorators.length - 1];
                keyToken = nullThrows(
                  context.sourceCode.getTokenAfter(lastDecorator),
                  NullThrowsReasons.MissingToken('key token', 'last decorator'),
                );
              }

              // if current token is a keyword like `static` or `public` then skip it
              while (
                keyToken.type === AST_TOKEN_TYPES.Keyword &&
                keyToken.range[0] < method.key.range[0]
              ) {
                keyToken = nullThrows(
                  context.sourceCode.getTokenAfter(keyToken),
                  NullThrowsReasons.MissingToken('token', 'keyword'),
                );
              }

              // check if there is a space between key and previous token
              const insertSpace = !context.sourceCode.isSpaceBetween(
                nullThrows(
                  context.sourceCode.getTokenBefore(keyToken),
                  NullThrowsReasons.MissingToken('token', 'keyword'),
                ),
                keyToken,
              );

              let code = 'async ';
              if (insertSpace) {
                code = ` ${code}`;
              }
              return fixer.insertTextBefore(keyToken, code);
            }

            return fixer.insertTextBefore(node, 'async ');
          }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `context.sourceCode.getTokenAfter`
  - `context.sourceCode.isSpaceBetween`
  - `context.sourceCode.getTokenBefore`
  - `fixer.insertTextBefore`
- **Internal Comments**:
```
// this function is a class method or object function property shorthand (x2)
// the token to put `async` before (x2)
// if there are decorators then skip past them
// if current token is a keyword like `static` or `public` then skip it
// check if there is a space between key and previous token (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
            if (
              node.parent.type === AST_NODE_TYPES.MethodDefinition ||
              (node.parent.type === AST_NODE_TYPES.Property &&
                node.parent.method)
            ) {
              // this function is a class method or object function property shorthand
              const method = node.parent;

              // the token to put `async` before
              let keyToken = nullThrows(
                context.sourceCode.getFirstToken(method),
                NullThrowsReasons.MissingToken('key token', 'method'),
              );

              // if there are decorators then skip past them
              if (
                method.type === AST_NODE_TYPES.MethodDefinition &&
                method.decorators.length
              ) {
                const lastDecorator =
                  method.decorators[method.decorators.length - 1];
                keyToken = nullThrows(
                  context.sourceCode.getTokenAfter(lastDecorator),
                  NullThrowsReasons.MissingToken('key token', 'last decorator'),
                );
              }

              // if current token is a keyword like `static` or `public` then skip it
              while (
                keyToken.type === AST_TOKEN_TYPES.Keyword &&
                keyToken.range[0] < method.key.range[0]
              ) {
                keyToken = nullThrows(
                  context.sourceCode.getTokenAfter(keyToken),
                  NullThrowsReasons.MissingToken('token', 'keyword'),
                );
              }

              // check if there is a space between key and previous token
              const insertSpace = !context.sourceCode.isSpaceBetween(
                nullThrows(
                  context.sourceCode.getTokenBefore(keyToken),
                  NullThrowsReasons.MissingToken('token', 'keyword'),
                ),
                keyToken,
              );

              let code = 'async ';
              if (insertSpace) {
                code = ` ${code}`;
              }
              return fixer.insertTextBefore(keyToken, code);
            }

            return fixer.insertTextBefore(node, 'async ');
          }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `context.sourceCode.getTokenAfter`
  - `context.sourceCode.isSpaceBetween`
  - `context.sourceCode.getTokenBefore`
  - `fixer.insertTextBefore`
- **Internal Comments**:
```
// this function is a class method or object function property shorthand (x2)
// the token to put `async` before (x2)
// if there are decorators then skip past them
// if current token is a keyword like `static` or `public` then skip it
// check if there is a space between key and previous token (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
            if (
              node.parent.type === AST_NODE_TYPES.MethodDefinition ||
              (node.parent.type === AST_NODE_TYPES.Property &&
                node.parent.method)
            ) {
              // this function is a class method or object function property shorthand
              const method = node.parent;

              // the token to put `async` before
              let keyToken = nullThrows(
                context.sourceCode.getFirstToken(method),
                NullThrowsReasons.MissingToken('key token', 'method'),
              );

              // if there are decorators then skip past them
              if (
                method.type === AST_NODE_TYPES.MethodDefinition &&
                method.decorators.length
              ) {
                const lastDecorator =
                  method.decorators[method.decorators.length - 1];
                keyToken = nullThrows(
                  context.sourceCode.getTokenAfter(lastDecorator),
                  NullThrowsReasons.MissingToken('key token', 'last decorator'),
                );
              }

              // if current token is a keyword like `static` or `public` then skip it
              while (
                keyToken.type === AST_TOKEN_TYPES.Keyword &&
                keyToken.range[0] < method.key.range[0]
              ) {
                keyToken = nullThrows(
                  context.sourceCode.getTokenAfter(keyToken),
                  NullThrowsReasons.MissingToken('token', 'keyword'),
                );
              }

              // check if there is a space between key and previous token
              const insertSpace = !context.sourceCode.isSpaceBetween(
                nullThrows(
                  context.sourceCode.getTokenBefore(keyToken),
                  NullThrowsReasons.MissingToken('token', 'keyword'),
                ),
                keyToken,
              );

              let code = 'async ';
              if (insertSpace) {
                code = ` ${code}`;
              }
              return fixer.insertTextBefore(keyToken, code);
            }

            return fixer.insertTextBefore(node, 'async ');
          }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `context.sourceCode.getTokenAfter`
  - `context.sourceCode.isSpaceBetween`
  - `context.sourceCode.getTokenBefore`
  - `fixer.insertTextBefore`
- **Internal Comments**:
```
// this function is a class method or object function property shorthand (x2)
// the token to put `async` before (x2)
// if there are decorators then skip past them
// if current token is a keyword like `static` or `public` then skip it
// check if there is a space between key and previous token (x2)
```


---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    allowAny?: boolean;
    allowedPromiseNames?: string[];
    checkArrowFunctions?: boolean;
    checkFunctionDeclarations?: boolean;
    checkFunctionExpressions?: boolean;
    checkMethodDeclarations?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'missingAsync' | 'missingAsyncHybridReturn';
```


---