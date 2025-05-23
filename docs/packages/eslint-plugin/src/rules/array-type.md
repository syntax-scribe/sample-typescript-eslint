[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `array-type.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/array-type.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `isParenthesized` | `../util` |


---

## Functions

### `isSimpleType(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isSimpleType(node: TSESTree.Node): boolean {
  switch (node.type) {
    case AST_NODE_TYPES.Identifier:
    case AST_NODE_TYPES.TSAnyKeyword:
    case AST_NODE_TYPES.TSBooleanKeyword:
    case AST_NODE_TYPES.TSNeverKeyword:
    case AST_NODE_TYPES.TSNumberKeyword:
    case AST_NODE_TYPES.TSBigIntKeyword:
    case AST_NODE_TYPES.TSObjectKeyword:
    case AST_NODE_TYPES.TSStringKeyword:
    case AST_NODE_TYPES.TSSymbolKeyword:
    case AST_NODE_TYPES.TSUnknownKeyword:
    case AST_NODE_TYPES.TSVoidKeyword:
    case AST_NODE_TYPES.TSNullKeyword:
    case AST_NODE_TYPES.TSArrayType:
    case AST_NODE_TYPES.TSUndefinedKeyword:
    case AST_NODE_TYPES.TSThisType:
    case AST_NODE_TYPES.TSQualifiedName:
      return true;
    case AST_NODE_TYPES.TSTypeReference:
      if (
        node.typeName.type === AST_NODE_TYPES.Identifier &&
        node.typeName.name === 'Array'
      ) {
        if (!node.typeArguments) {
          return true;
        }
        if (node.typeArguments.params.length === 1) {
          return isSimpleType(node.typeArguments.params[0]);
        }
      } else {
        if (node.typeArguments) {
          return false;
        }
        return isSimpleType(node.typeName);
      }
      return false;
    default:
      return false;
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check whatever node can be considered as simple
 * @param node the node to be evaluated.
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isSimpleType`
### `typeNeedsParentheses(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function typeNeedsParentheses(node: TSESTree.Node): boolean {
  switch (node.type) {
    case AST_NODE_TYPES.TSTypeReference:
      return typeNeedsParentheses(node.typeName);
    case AST_NODE_TYPES.TSUnionType:
    case AST_NODE_TYPES.TSFunctionType:
    case AST_NODE_TYPES.TSIntersectionType:
    case AST_NODE_TYPES.TSTypeOperator:
    case AST_NODE_TYPES.TSInferType:
    case AST_NODE_TYPES.TSConstructorType:
    case AST_NODE_TYPES.TSConditionalType:
      return true;
    case AST_NODE_TYPES.Identifier:
      return node.name === 'ReadonlyArray';
    default:
      return false;
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if node needs parentheses
 * @param node the node to be evaluated.
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `typeNeedsParentheses`
### `getMessageType(node: TSESTree.Node): string`

<details><summary>Code</summary>

```ts
function getMessageType(node: TSESTree.Node): string {
      if (isSimpleType(node)) {
        return context.sourceCode.getText(node);
      }
      return 'T';
    }
```
</details>

- **JSDoc**:
```ts
/**
     * @param node the node to be evaluated.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `string`
- **Calls**:
  - `isSimpleType`
  - `context.sourceCode.getText`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `OptionString`

```ts
type OptionString = 'array' | 'array-simple' | 'generic';
```

### `Options`

```ts
type Options = [
  {
    default: OptionString;
    readonly?: OptionString;
  },
];
```

### `MessageIds`

```ts
type MessageIds = | 'errorStringArray'
  | 'errorStringArrayReadonly'
  | 'errorStringArraySimple'
  | 'errorStringArraySimpleReadonly'
  | 'errorStringGeneric'
  | 'errorStringGenericSimple';
```


---