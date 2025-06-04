[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `array-type.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 18 |
| 📑 Type Aliases | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `defaultOption` | `any` | const | `options.default` | ✗ |
| `readonlyOption` | `any` | const | `options.readonly ?? defaultOption` | ✗ |
| `isReadonly` | `boolean` | const | `node.parent.type === AST_NODE_TYPES.TSTypeOperator &&
          node.parent.operator === 'readonly'` | ✗ |
| `currentOption` | `any` | const | `isReadonly ? readonlyOption : defaultOption` | ✗ |
| `messageId` | `"errorStringGeneric" | "errorStringGenericSimple"` | const | `currentOption === 'generic'
            ? 'errorStringGeneric'
            : 'errorStringGenericSimple'` | ✗ |
| `errorNode` | `any` | const | `isReadonly ? node.parent : node` | ✗ |
| `typeNode` | `any` | const | `node.elementType` | ✗ |
| `arrayType` | `"ReadonlyArray" | "Array"` | const | `isReadonly ? 'ReadonlyArray' : 'Array'` | ✗ |
| `isReadonlyWithGenericArrayType` | `boolean` | const | `node.typeName.name === 'Readonly' &&
          node.typeArguments?.params[0].type === AST_NODE_TYPES.TSArrayType` | ✗ |
| `isReadonlyArrayType` | `boolean` | const | `node.typeName.name === 'ReadonlyArray' ||
          isReadonlyWithGenericArrayType` | ✗ |
| `currentOption` | `any` | const | `isReadonlyArrayType
          ? readonlyOption
          : defaultOption` | ✗ |
| `readonlyPrefix` | `"" | "readonly "` | const | `isReadonlyArrayType ? 'readonly ' : ''` | ✗ |
| `typeParams` | `any` | const | `node.typeArguments?.params` | ✗ |
| `messageId` | `"errorStringArray" | "errorStringArrayReadonly" | "errorStringArraySimple" | "errorStringArraySimpleReadonly"` | const | `currentOption === 'array'
            ? isReadonlyWithGenericArrayType
              ? 'errorStringArrayReadonly'
              : 'errorStringArray'
            : isReadonlyArrayType && node.typeName.name !== 'ReadonlyArray'
              ? 'errorStringArraySimpleReadonly'
              : 'errorStringArraySimple'` | ✗ |
| `type` | `any` | const | `typeParams[0]` | ✗ |
| `parentParens` | `boolean` | const | `readonlyPrefix &&
          node.parent.type === AST_NODE_TYPES.TSArrayType &&
          !isParenthesized(node.parent.elementType, context.sourceCode)` | ✗ |
| `start` | `string` | const | ``${parentParens ? '(' : ''}${readonlyPrefix}${
          typeParens ? '(' : ''
        }`` | ✗ |
| `end` | `string` | const | ``${typeParens ? ')' : ''}${isReadonlyWithGenericArrayType ? '' : `[]`}${parentParens ? ')' : ''}`` | ✗ |


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