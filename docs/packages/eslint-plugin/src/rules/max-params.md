[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `max-params.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 4

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/max-params.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---

## Functions

### `removeVoidThisParam(node: T): T`

<details><summary>Code</summary>

```ts
<T extends FunctionLike>(node: T): T => {
      if (
        node.params.length === 0 ||
        node.params[0].type !== AST_NODE_TYPES.Identifier ||
        node.params[0].name !== 'this' ||
        node.params[0].typeAnnotation?.typeAnnotation.type !==
          AST_NODE_TYPES.TSVoidKeyword
      ) {
        return node;
      }

      return {
        ...node,
        params: node.params.slice(1),
      };
    }
```
</details>

- **Parameters**:
  - `node: T`
- **Return Type**: `T`
- **Calls**:
  - `node.params.slice`
### `wrapListener(listener: FunctionRuleListener<T>): FunctionRuleListener<T>`

<details><summary>Code</summary>

```ts
<T extends FunctionLike>(
      listener: FunctionRuleListener<T>,
    ): FunctionRuleListener<T> => {
      return (node: T): void => {
        listener(removeVoidThisParam(node));
      };
    }
```
</details>

- **Parameters**:
  - `listener: FunctionRuleListener<T>`
- **Return Type**: `FunctionRuleListener<T>`
- **Calls**:
  - `listener`
  - `removeVoidThisParam`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `FunctionLike`

```ts
type FunctionLike = | TSESTree.ArrowFunctionExpression
  | TSESTree.FunctionDeclaration
  | TSESTree.FunctionExpression
  | TSESTree.TSDeclareFunction
  | TSESTree.TSFunctionType;
```

### `FunctionRuleListener<T extends FunctionLike extends FunctionLike>`

```ts
type FunctionRuleListener<T extends FunctionLike extends FunctionLike> = (node: T) => void;
```

### `Options`

```ts
type Options = InferOptionsTypeFromRule<typeof baseRule>;
```

### `MessageIds`

```ts
type MessageIds = InferMessageIdsTypeFromRule<typeof baseRule>;
```


---