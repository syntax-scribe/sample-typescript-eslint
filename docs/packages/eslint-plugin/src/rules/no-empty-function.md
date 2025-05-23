[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-empty-function.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 5
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-empty-function.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `deepMerge` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---

## Functions

### `isBodyEmpty(node: TSESTree.FunctionDeclaration | TSESTree.FunctionExpression): boolean`

<details><summary>Code</summary>

```ts
function isBodyEmpty(
      node: TSESTree.FunctionDeclaration | TSESTree.FunctionExpression,
    ): boolean {
      return node.body.body.length === 0;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if the method body is empty
     * @param node the node to be validated
     * @returns true if the body is empty
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.FunctionDeclaration | TSESTree.FunctionExpression`
- **Return Type**: `boolean`
### `hasParameterProperties(node: TSESTree.FunctionDeclaration | TSESTree.FunctionExpression): boolean`

<details><summary>Code</summary>

```ts
function hasParameterProperties(
      node: TSESTree.FunctionDeclaration | TSESTree.FunctionExpression,
    ): boolean {
      return node.params.some(
        param => param.type === AST_NODE_TYPES.TSParameterProperty,
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if method has parameter properties
     * @param node the node to be validated
     * @returns true if the body has parameter properties
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.FunctionDeclaration | TSESTree.FunctionExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `node.params.some`
### `isAllowedEmptyConstructor(node: TSESTree.FunctionDeclaration | TSESTree.FunctionExpression): boolean`

<details><summary>Code</summary>

```ts
function isAllowedEmptyConstructor(
      node: TSESTree.FunctionDeclaration | TSESTree.FunctionExpression,
    ): boolean {
      const parent = node.parent;
      if (
        isBodyEmpty(node) &&
        parent.type === AST_NODE_TYPES.MethodDefinition &&
        parent.kind === 'constructor'
      ) {
        const { accessibility } = parent;

        return (
          // allow protected constructors
          (accessibility === 'protected' && isAllowedProtectedConstructors) ||
          // allow private constructors
          (accessibility === 'private' && isAllowedPrivateConstructors) ||
          // allow constructors which have parameter properties
          hasParameterProperties(node)
        );
      }

      return false;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * @param node the node to be validated
     * @returns true if the constructor is allowed to be empty
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.FunctionDeclaration | TSESTree.FunctionExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `isBodyEmpty`
  - `hasParameterProperties`
- **Internal Comments**:
```
// allow protected constructors (x3)
// allow private constructors
// allow constructors which have parameter properties (x2)
```

### `isAllowedEmptyDecoratedFunctions(node: TSESTree.FunctionDeclaration | TSESTree.FunctionExpression): boolean`

<details><summary>Code</summary>

```ts
function isAllowedEmptyDecoratedFunctions(
      node: TSESTree.FunctionDeclaration | TSESTree.FunctionExpression,
    ): boolean {
      if (isAllowedDecoratedFunctions && isBodyEmpty(node)) {
        const decorators =
          node.parent.type === AST_NODE_TYPES.MethodDefinition
            ? node.parent.decorators
            : undefined;
        return !!decorators && !!decorators.length;
      }

      return false;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * @param node the node to be validated
     * @returns true if a function has decorators
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.FunctionDeclaration | TSESTree.FunctionExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `isBodyEmpty`
### `isAllowedEmptyOverrideMethod(node: TSESTree.FunctionExpression): boolean`

<details><summary>Code</summary>

```ts
function isAllowedEmptyOverrideMethod(
      node: TSESTree.FunctionExpression,
    ): boolean {
      return (
        isAllowedOverrideMethods &&
        isBodyEmpty(node) &&
        node.parent.type === AST_NODE_TYPES.MethodDefinition &&
        node.parent.override
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.FunctionExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `isBodyEmpty`

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
type Options = InferOptionsTypeFromRule<typeof baseRule>;
```

### `MessageIds`

```ts
type MessageIds = InferMessageIdsTypeFromRule<typeof baseRule>;
```


---