[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-extraneous-class.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-extraneous-class.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `isAllowWithDecorator(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression | undefined): boolean`

<details><summary>Code</summary>

```ts
(
      node: TSESTree.ClassDeclaration | TSESTree.ClassExpression | undefined,
    ): boolean => {
      return !!(
        allowWithDecorator &&
        node?.decorators &&
        node.decorators.length !== 0
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression | undefined`
- **Return Type**: `boolean`

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
type Options = [
  {
    allowConstructorOnly?: boolean;
    allowEmpty?: boolean;
    allowStaticOnly?: boolean;
    allowWithDecorator?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'empty' | 'onlyConstructor' | 'onlyStatic';
```


---