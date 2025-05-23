[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `promiseUtils.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/promiseUtils.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleContext` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `getStaticMemberAccessValue` | `./misc` |


---

## Functions

### `parseThenCall(node: TSESTree.CallExpression, context: RuleContext<string, unknown[]>): | {
      onFulfilled?: TSESTree.Expression | undefined;
      onRejected?: TSESTree.Expression | undefined;
      object: TSESTree.Expression;
    }
  | undefined`

<details><summary>Code</summary>

```ts
export function parseThenCall(
  node: TSESTree.CallExpression,
  context: RuleContext<string, unknown[]>,
):
  | {
      onFulfilled?: TSESTree.Expression | undefined;
      onRejected?: TSESTree.Expression | undefined;
      object: TSESTree.Expression;
    }
  | undefined {
  if (node.callee.type === AST_NODE_TYPES.MemberExpression) {
    const methodName = getStaticMemberAccessValue(node.callee, context);
    if (methodName === 'then') {
      if (node.arguments.length >= 1) {
        if (node.arguments[0].type === AST_NODE_TYPES.SpreadElement) {
          return {
            object: node.callee.object,
          };
        }

        if (node.arguments.length >= 2) {
          if (node.arguments[1].type === AST_NODE_TYPES.SpreadElement) {
            return {
              object: node.callee.object,
              onFulfilled: node.arguments[0],
            };
          }

          return {
            object: node.callee.object,
            onFulfilled: node.arguments[0],
            onRejected: node.arguments[1],
          };
        }
        return {
          object: node.callee.object,
          onFulfilled: node.arguments[0],
        };
      }
      return {
        object: node.callee.object,
      };
    }
  }

  return undefined;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Parses a syntactically possible `Promise.then()` call. Does not check the
 * type of the callee.
 */
```

- **Parameters**:
  - `node: TSESTree.CallExpression`
  - `context: RuleContext<string, unknown[]>`
- **Return Type**: `| {
      onFulfilled?: TSESTree.Expression | undefined;
      onRejected?: TSESTree.Expression | undefined;
      object: TSESTree.Expression;
    }
  | undefined`
- **Calls**:
  - `getStaticMemberAccessValue (from ./misc)`
### `parseCatchCall(node: TSESTree.CallExpression, context: RuleContext<string, unknown[]>): | {
      onRejected?: TSESTree.Expression | undefined;
      object: TSESTree.Expression;
    }
  | undefined`

<details><summary>Code</summary>

```ts
export function parseCatchCall(
  node: TSESTree.CallExpression,
  context: RuleContext<string, unknown[]>,
):
  | {
      onRejected?: TSESTree.Expression | undefined;
      object: TSESTree.Expression;
    }
  | undefined {
  if (node.callee.type === AST_NODE_TYPES.MemberExpression) {
    const methodName = getStaticMemberAccessValue(node.callee, context);
    if (methodName === 'catch') {
      if (node.arguments.length >= 1) {
        if (node.arguments[0].type === AST_NODE_TYPES.SpreadElement) {
          return {
            object: node.callee.object,
          };
        }

        return {
          object: node.callee.object,
          onRejected: node.arguments[0],
        };
      }
      return {
        object: node.callee.object,
      };
    }
  }

  return undefined;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Parses a syntactically possible `Promise.catch()` call. Does not check the
 * type of the callee.
 */
```

- **Parameters**:
  - `node: TSESTree.CallExpression`
  - `context: RuleContext<string, unknown[]>`
- **Return Type**: `| {
      onRejected?: TSESTree.Expression | undefined;
      object: TSESTree.Expression;
    }
  | undefined`
- **Calls**:
  - `getStaticMemberAccessValue (from ./misc)`
### `parseFinallyCall(node: TSESTree.CallExpression, context: RuleContext<string, unknown[]>): | {
      object: TSESTree.Expression;
      onFinally?: TSESTree.Expression | undefined;
    }
  | undefined`

<details><summary>Code</summary>

```ts
export function parseFinallyCall(
  node: TSESTree.CallExpression,
  context: RuleContext<string, unknown[]>,
):
  | {
      object: TSESTree.Expression;
      onFinally?: TSESTree.Expression | undefined;
    }
  | undefined {
  if (node.callee.type === AST_NODE_TYPES.MemberExpression) {
    const methodName = getStaticMemberAccessValue(node.callee, context);
    if (methodName === 'finally') {
      if (node.arguments.length >= 1) {
        if (node.arguments[0].type === AST_NODE_TYPES.SpreadElement) {
          return {
            object: node.callee.object,
          };
        }
        return {
          object: node.callee.object,
          onFinally: node.arguments[0],
        };
      }
      return {
        object: node.callee.object,
      };
    }
  }

  return undefined;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Parses a syntactically possible `Promise.finally()` call. Does not check the
 * type of the callee.
 */
```

- **Parameters**:
  - `node: TSESTree.CallExpression`
  - `context: RuleContext<string, unknown[]>`
- **Return Type**: `| {
      object: TSESTree.Expression;
      onFinally?: TSESTree.Expression | undefined;
    }
  | undefined`
- **Calls**:
  - `getStaticMemberAccessValue (from ./misc)`

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