[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-redundant-type-constituents.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 10
- **Classes**: 0
- **Imports**: 11
- **Interfaces**: 3
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-redundant-type-constituents.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `arrayGroupByToMap` | `../util` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `isFunctionOrFunctionType` | `../util` |
| `isTypeAnyType` | `../util` |
| `isTypeBigIntLiteralType` | `../util` |
| `isTypeNeverType` | `../util` |
| `isTypeTemplateLiteralType` | `../util` |
| `isTypeUnknownType` | `../util` |


---

## Functions

### `addToMapGroup(map: Map<Key, Value[]>, key: Key, value: Value): void`

<details><summary>Code</summary>

```ts
function addToMapGroup<Key, Value>(
  map: Map<Key, Value[]>,
  key: Key,
  value: Value,
): void {
  const existing = map.get(key);

  if (existing) {
    existing.push(value);
  } else {
    map.set(key, [value]);
  }
}
```
</details>

- **Parameters**:
  - `map: Map<Key, Value[]>`
  - `key: Key`
  - `value: Value`
- **Return Type**: `void`
- **Calls**:
  - `map.get`
  - `existing.push`
  - `map.set`
### `describeLiteralType(type: ts.Type): string`

<details><summary>Code</summary>

```ts
function describeLiteralType(type: ts.Type): string {
  if (type.isStringLiteral()) {
    return JSON.stringify(type.value);
  }

  if (isTypeBigIntLiteralType(type)) {
    return `${type.value.negative ? '-' : ''}${type.value.base10Value}n`;
  }

  if (type.isLiteral()) {
    // eslint-disable-next-line @typescript-eslint/no-base-to-string
    return type.value.toString();
  }

  if (tsutils.isIntrinsicErrorType(type) && type.aliasSymbol) {
    return type.aliasSymbol.escapedName.toString();
  }

  if (isTypeAnyType(type)) {
    return 'any';
  }

  if (isTypeNeverType(type)) {
    return 'never';
  }

  if (isTypeUnknownType(type)) {
    return 'unknown';
  }

  if (isTypeTemplateLiteralType(type)) {
    return 'template literal type';
  }

  if (isTypeBigIntLiteralType(type)) {
    return `${type.value.negative ? '-' : ''}${type.value.base10Value}n`;
  }

  if (tsutils.isTrueLiteralType(type)) {
    return 'true';
  }

  if (tsutils.isFalseLiteralType(type)) {
    return 'false';
  }

  return 'literal type';
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `string`
- **Calls**:
  - `type.isStringLiteral`
  - `JSON.stringify`
  - `isTypeBigIntLiteralType (from ../util)`
  - `type.isLiteral`
  - `type.value.toString`
  - `tsutils.isIntrinsicErrorType`
  - `type.aliasSymbol.escapedName.toString`
  - `isTypeAnyType (from ../util)`
  - `isTypeNeverType (from ../util)`
  - `isTypeUnknownType (from ../util)`
  - `isTypeTemplateLiteralType (from ../util)`
  - `tsutils.isTrueLiteralType`
  - `tsutils.isFalseLiteralType`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-base-to-string
```

### `describeLiteralTypeNode(typeNode: TSESTree.TypeNode): string`

<details><summary>Code</summary>

```ts
function describeLiteralTypeNode(typeNode: TSESTree.TypeNode): string {
  switch (typeNode.type) {
    case AST_NODE_TYPES.TSAnyKeyword:
      return 'any';
    case AST_NODE_TYPES.TSBooleanKeyword:
      return 'boolean';
    case AST_NODE_TYPES.TSNeverKeyword:
      return 'never';
    case AST_NODE_TYPES.TSNumberKeyword:
      return 'number';
    case AST_NODE_TYPES.TSStringKeyword:
      return 'string';
    case AST_NODE_TYPES.TSUnknownKeyword:
      return 'unknown';
    case AST_NODE_TYPES.TSLiteralType:
      switch (typeNode.literal.type) {
        case TSESTree.AST_NODE_TYPES.Literal:
          switch (typeof typeNode.literal.value) {
            case 'bigint':
              return `${typeNode.literal.value < 0 ? '-' : ''}${
                typeNode.literal.value
              }n`;
            case 'string':
              return JSON.stringify(typeNode.literal.value);
            default:
              return `${typeNode.literal.value}`;
          }
        case TSESTree.AST_NODE_TYPES.TemplateLiteral:
          return 'template literal type';
      }
  }

  return 'literal type';
}
```
</details>

- **Parameters**:
  - `typeNode: TSESTree.TypeNode`
- **Return Type**: `string`
- **Calls**:
  - `JSON.stringify`
### `isNodeInsideReturnType(node: TSESTree.TSUnionType): boolean`

<details><summary>Code</summary>

```ts
function isNodeInsideReturnType(node: TSESTree.TSUnionType): boolean {
  return (
    node.parent.type === AST_NODE_TYPES.TSTypeAnnotation &&
    isFunctionOrFunctionType(node.parent.parent)
  );
}
```
</details>

- **Parameters**:
  - `node: TSESTree.TSUnionType`
- **Return Type**: `boolean`
- **Calls**:
  - `isFunctionOrFunctionType (from ../util)`
### `unionTypePartsUnlessBoolean(type: ts.Type): ts.Type[]`

<details><summary>Code</summary>

```ts
function unionTypePartsUnlessBoolean(type: ts.Type): ts.Type[] {
  return type.isUnion() &&
    type.types.length === 2 &&
    tsutils.isFalseLiteralType(type.types[0]) &&
    tsutils.isTrueLiteralType(type.types[1])
    ? [type]
    : tsutils.unionConstituents(type);
}
```
</details>

- **JSDoc**:
```ts
/**
 * @remarks TypeScript stores boolean types as the union false | true, always.
 */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `ts.Type[]`
- **Calls**:
  - `type.isUnion`
  - `tsutils.isFalseLiteralType`
  - `tsutils.isTrueLiteralType`
  - `tsutils.unionConstituents`
### `getTypeNodeTypePartFlags(typeNode: TSESTree.TypeNode): TypeFlagsWithName[]`

<details><summary>Code</summary>

```ts
function getTypeNodeTypePartFlags(
      typeNode: TSESTree.TypeNode,
    ): TypeFlagsWithName[] {
      const keywordTypeFlags = keywordNodeTypesToTsTypes.get(typeNode.type);
      if (keywordTypeFlags) {
        return [
          {
            typeFlags: keywordTypeFlags,
            typeName: describeLiteralTypeNode(typeNode),
          },
        ];
      }

      if (
        typeNode.type === AST_NODE_TYPES.TSLiteralType &&
        typeNode.literal.type === AST_NODE_TYPES.Literal
      ) {
        return [
          {
            typeFlags:
              primitiveTypeFlagTypes[
                typeof typeNode.literal
                  .value as keyof typeof primitiveTypeFlagTypes
              ],
            typeName: describeLiteralTypeNode(typeNode),
          },
        ];
      }

      if (typeNode.type === AST_NODE_TYPES.TSUnionType) {
        return typeNode.types.flatMap(getTypeNodeTypePartFlags);
      }

      const nodeType = services.getTypeAtLocation(typeNode);
      const typeParts = unionTypePartsUnlessBoolean(nodeType);

      return typeParts.map(typePart => ({
        typeFlags: typePart.flags,
        typeName: describeLiteralType(typePart),
      }));
    }
```
</details>

- **Parameters**:
  - `typeNode: TSESTree.TypeNode`
- **Return Type**: `TypeFlagsWithName[]`
- **Calls**:
  - `keywordNodeTypesToTsTypes.get`
  - `describeLiteralTypeNode`
  - `typeNode.types.flatMap`
  - `services.getTypeAtLocation`
  - `unionTypePartsUnlessBoolean`
  - `typeParts.map`
  - `describeLiteralType`
### `getTypeNodeTypePartFlagsCached(typeNode: TSESTree.TypeNode): TypeFlagsWithName[]`

<details><summary>Code</summary>

```ts
function getTypeNodeTypePartFlagsCached(
      typeNode: TSESTree.TypeNode,
    ): TypeFlagsWithName[] {
      const existing = typesCache.get(typeNode);
      if (existing) {
        return existing;
      }

      const created = getTypeNodeTypePartFlags(typeNode);
      typesCache.set(typeNode, created);
      return created;
    }
```
</details>

- **Parameters**:
  - `typeNode: TSESTree.TypeNode`
- **Return Type**: `TypeFlagsWithName[]`
- **Calls**:
  - `typesCache.get`
  - `getTypeNodeTypePartFlags`
  - `typesCache.set`
### `checkIntersectionBottomAndTopTypes({ typeFlags, typeName }: TypeFlagsWithName, typeNode: TSESTree.TypeNode): boolean`

<details><summary>Code</summary>

```ts
function checkIntersectionBottomAndTopTypes(
          { typeFlags, typeName }: TypeFlagsWithName,
          typeNode: TSESTree.TypeNode,
        ): boolean {
          for (const [messageId, checkFlag] of [
            ['overrides', ts.TypeFlags.Any],
            ['overrides', ts.TypeFlags.Never],
            ['overridden', ts.TypeFlags.Unknown],
          ] as const) {
            if (typeFlags === checkFlag) {
              context.report({
                node: typeNode,
                messageId:
                  typeFlags === ts.TypeFlags.Any && typeName !== 'any'
                    ? 'errorTypeOverrides'
                    : messageId,
                data: {
                  container: 'intersection',
                  typeName,
                },
              });
              return true;
            }
          }

          return false;
        }
```
</details>

- **Parameters**:
  - `{ typeFlags, typeName }: TypeFlagsWithName`
  - `typeNode: TSESTree.TypeNode`
- **Return Type**: `boolean`
- **Calls**:
  - `context.report`
### `checkIfUnionsAreAssignable(): undefined`

<details><summary>Code</summary>

```ts
(): undefined => {
          for (const [typeRef, typeValues] of seenUnionTypes) {
            let primitive: number | undefined = undefined;
            for (const { typeFlags } of typeValues) {
              if (
                seenPrimitiveTypes.has(
                  literalToPrimitiveTypeFlags[
                    typeFlags as keyof typeof literalToPrimitiveTypeFlags
                  ],
                )
              ) {
                primitive =
                  literalToPrimitiveTypeFlags[
                    typeFlags as keyof typeof literalToPrimitiveTypeFlags
                  ];
              } else {
                primitive = undefined;
                break;
              }
            }
            if (Number.isInteger(primitive)) {
              context.report({
                node: typeRef,
                messageId: 'primitiveOverridden',
                data: {
                  literal: typeValues.map(name => name.typeName).join(' | '),
                  primitive:
                    primitiveTypeFlagNames[
                      primitive as keyof typeof primitiveTypeFlagNames
                    ],
                },
              });
            }
          }
        }
```
</details>

- **Return Type**: `undefined`
- **Calls**:
  - `seenPrimitiveTypes.has`
  - `Number.isInteger`
  - `context.report`
  - `typeValues.map(name => name.typeName).join`
### `checkUnionBottomAndTopTypes({ typeFlags, typeName }: TypeFlagsWithName, typeNode: TSESTree.TypeNode): boolean`

<details><summary>Code</summary>

```ts
function checkUnionBottomAndTopTypes(
          { typeFlags, typeName }: TypeFlagsWithName,
          typeNode: TSESTree.TypeNode,
        ): boolean {
          for (const checkFlag of [
            ts.TypeFlags.Any,
            ts.TypeFlags.Unknown,
          ] as const) {
            if (typeFlags === checkFlag) {
              context.report({
                node: typeNode,
                messageId:
                  typeFlags === ts.TypeFlags.Any && typeName !== 'any'
                    ? 'errorTypeOverrides'
                    : 'overrides',
                data: {
                  container: 'union',
                  typeName,
                },
              });
              return true;
            }
          }

          if (
            typeFlags === ts.TypeFlags.Never &&
            !isNodeInsideReturnType(node)
          ) {
            context.report({
              node: typeNode,
              messageId: 'overridden',
              data: {
                container: 'union',
                typeName: 'never',
              },
            });
            return true;
          }

          return false;
        }
```
</details>

- **Parameters**:
  - `{ typeFlags, typeName }: TypeFlagsWithName`
  - `typeNode: TSESTree.TypeNode`
- **Return Type**: `boolean`
- **Calls**:
  - `context.report`
  - `isNodeInsideReturnType`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `TypeFlagsWithName`

<details><summary>Interface Code</summary>

```ts
interface TypeFlagsWithName {
  typeFlags: ts.TypeFlags;
  typeName: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `typeFlags` | `ts.TypeFlags` | ✗ |  |
| `typeName` | `string` | ✗ |  |

### `TypeNodeWithValue`

<details><summary>Interface Code</summary>

```ts
interface TypeNodeWithValue {
  literalValue: unknown;
  typeNode: TSESTree.TypeNode;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `literalValue` | `unknown` | ✗ |  |
| `typeNode` | `TSESTree.TypeNode` | ✗ |  |

### `TypeFlagWithText`

<details><summary>Interface Code</summary>

```ts
interface TypeFlagWithText {
          literalValue: unknown;
          primitiveTypeFlag: PrimitiveTypeFlag;
        }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `literalValue` | `unknown` | ✗ |  |
| `primitiveTypeFlag` | `PrimitiveTypeFlag` | ✗ |  |


---

## Type Aliases

### `PrimitiveTypeFlag`

```ts
type PrimitiveTypeFlag = (typeof primitiveTypeFlags)[number];
```


---