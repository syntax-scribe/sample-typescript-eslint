[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `default-param-last.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/default-param-last.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `isOptionalParam(node: TSESTree.Parameter): boolean`

<details><summary>Code</summary>

```ts
function isOptionalParam(node: TSESTree.Parameter): boolean {
      return (
        (node.type === AST_NODE_TYPES.ArrayPattern ||
          node.type === AST_NODE_TYPES.AssignmentPattern ||
          node.type === AST_NODE_TYPES.Identifier ||
          node.type === AST_NODE_TYPES.ObjectPattern ||
          node.type === AST_NODE_TYPES.RestElement) &&
        node.optional
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * checks if node is optional parameter
     * @param node the node to be evaluated
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.Parameter`
- **Return Type**: `boolean`
### `isPlainParam(node: TSESTree.Parameter): boolean`

<details><summary>Code</summary>

```ts
function isPlainParam(node: TSESTree.Parameter): boolean {
      return !(
        node.type === AST_NODE_TYPES.AssignmentPattern ||
        node.type === AST_NODE_TYPES.RestElement ||
        isOptionalParam(node)
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * checks if node is plain parameter
     * @param node the node to be evaluated
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.Parameter`
- **Return Type**: `boolean`
- **Calls**:
  - `isOptionalParam`
### `checkDefaultParamLast(node: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression): void`

<details><summary>Code</summary>

```ts
function checkDefaultParamLast(
      node:
        | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression,
    ): void {
      let hasSeenPlainParam = false;
      for (let i = node.params.length - 1; i >= 0; i--) {
        const current = node.params[i];
        const param =
          current.type === AST_NODE_TYPES.TSParameterProperty
            ? current.parameter
            : current;

        if (isPlainParam(param)) {
          hasSeenPlainParam = true;
          continue;
        }

        if (
          hasSeenPlainParam &&
          (isOptionalParam(param) ||
            param.type === AST_NODE_TYPES.AssignmentPattern)
        ) {
          context.report({ node: current, messageId: 'shouldBeLast' });
        }
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
  - `isPlainParam`
  - `isOptionalParam`
  - `context.report`

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