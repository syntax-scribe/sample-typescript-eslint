[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-type-alias.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 7
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 1
- **Type Aliases**: 4

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-type-alias.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `isSupportedComposition(isTopLevel: boolean, compositionType: CompositionType | null, allowed: string): boolean`

<details><summary>Code</summary>

```ts
function isSupportedComposition(
      isTopLevel: boolean,
      compositionType: CompositionType | null,
      allowed: string,
    ): boolean {
      return (
        !compositions.includes(allowed) ||
        (!isTopLevel &&
          ((compositionType === AST_NODE_TYPES.TSUnionType &&
            unions.includes(allowed)) ||
            (compositionType === AST_NODE_TYPES.TSIntersectionType &&
              intersections.includes(allowed))))
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Determines if the composition type is supported by the allowed flags.
     * @param isTopLevel a flag indicating this is the top level node.
     * @param compositionType the composition type (either TSUnionType or TSIntersectionType)
     * @param allowed the currently allowed flags.
     */
```

- **Parameters**:
  - `isTopLevel: boolean`
  - `compositionType: CompositionType | null`
  - `allowed: string`
- **Return Type**: `boolean`
- **Calls**:
  - `compositions.includes`
  - `unions.includes`
  - `intersections.includes`
### `reportError(node: TSESTree.Node, compositionType: CompositionType | null, isRoot: boolean, type: string): void`

<details><summary>Code</summary>

```ts
function reportError(
      node: TSESTree.Node,
      compositionType: CompositionType | null,
      isRoot: boolean,
      type: string,
    ): void {
      if (isRoot) {
        return context.report({
          node,
          messageId: 'noTypeAlias',
          data: {
            alias: type.toLowerCase(),
          },
        });
      }

      return context.report({
        node,
        messageId: 'noCompositionAlias',
        data: {
          compositionType:
            compositionType === AST_NODE_TYPES.TSUnionType
              ? 'union'
              : 'intersection',
          typeName: type,
        },
      });
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Gets the message to be displayed based on the node type and whether the node is a top level declaration.
     * @param node the location
     * @param compositionType the type of composition this alias is part of (undefined if not
     *                                  part of a composition)
     * @param isRoot a flag indicating we are dealing with the top level declaration.
     * @param type the kind of type alias being validated.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `compositionType: CompositionType | null`
  - `isRoot: boolean`
  - `type: string`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `type.toLowerCase`
### `isValidTupleType(type: TypeWithLabel): boolean`

<details><summary>Code</summary>

```ts
(type: TypeWithLabel): boolean => {
      if (type.node.type === AST_NODE_TYPES.TSTupleType) {
        return true;
      }
      if (
        type.node.type === AST_NODE_TYPES.TSTypeOperator &&
        ['keyof', 'readonly'].includes(type.node.operator) &&
        type.node.typeAnnotation &&
        type.node.typeAnnotation.type === AST_NODE_TYPES.TSTupleType
      ) {
        return true;
      }
      return false;
    }
```
</details>

- **Parameters**:
  - `type: TypeWithLabel`
- **Return Type**: `boolean`
- **Calls**:
  - `['keyof', 'readonly'].includes`
### `isValidGeneric(type: TypeWithLabel): boolean`

<details><summary>Code</summary>

```ts
(type: TypeWithLabel): boolean => {
      return (
        type.node.type === AST_NODE_TYPES.TSTypeReference &&
        type.node.typeArguments != null
      );
    }
```
</details>

- **Parameters**:
  - `type: TypeWithLabel`
- **Return Type**: `boolean`
### `checkAndReport(optionValue: Values, isTopLevel: boolean, type: TypeWithLabel, label: string): void`

<details><summary>Code</summary>

```ts
(
      optionValue: Values,
      isTopLevel: boolean,
      type: TypeWithLabel,
      label: string,
    ): void => {
      if (
        optionValue === 'never' ||
        !isSupportedComposition(isTopLevel, type.compositionType, optionValue)
      ) {
        reportError(type.node, type.compositionType, isTopLevel, label);
      }
    }
```
</details>

- **Parameters**:
  - `optionValue: Values`
  - `isTopLevel: boolean`
  - `type: TypeWithLabel`
  - `label: string`
- **Return Type**: `void`
- **Calls**:
  - `isSupportedComposition`
  - `reportError`
### `validateTypeAliases(type: TypeWithLabel, isTopLevel: boolean): void`

<details><summary>Code</summary>

```ts
function validateTypeAliases(
      type: TypeWithLabel,
      isTopLevel = false,
    ): void {
      // https://github.com/typescript-eslint/typescript-eslint/issues/5439
      /* eslint-disable @typescript-eslint/no-non-null-assertion */
      if (type.node.type === AST_NODE_TYPES.TSFunctionType) {
        // callback
        if (allowCallbacks === 'never') {
          reportError(type.node, type.compositionType, isTopLevel, 'Callbacks');
        }
      } else if (type.node.type === AST_NODE_TYPES.TSConditionalType) {
        // conditional type
        if (allowConditionalTypes === 'never') {
          reportError(
            type.node,
            type.compositionType,
            isTopLevel,
            'Conditional types',
          );
        }
      } else if (type.node.type === AST_NODE_TYPES.TSConstructorType) {
        if (allowConstructors === 'never') {
          reportError(
            type.node,
            type.compositionType,
            isTopLevel,
            'Constructors',
          );
        }
      } else if (type.node.type === AST_NODE_TYPES.TSTypeLiteral) {
        // literal object type
        checkAndReport(allowLiterals!, isTopLevel, type, 'Literals');
      } else if (type.node.type === AST_NODE_TYPES.TSMappedType) {
        // mapped type
        checkAndReport(allowMappedTypes!, isTopLevel, type, 'Mapped types');
      } else if (isValidTupleType(type)) {
        // tuple types
        checkAndReport(allowTupleTypes!, isTopLevel, type, 'Tuple Types');
      } else if (isValidGeneric(type)) {
        if (allowGenerics === 'never') {
          reportError(type.node, type.compositionType, isTopLevel, 'Generics');
        }
      } else if (
        type.node.type.endsWith(AST_TOKEN_TYPES.Keyword) ||
        aliasTypes.has(type.node.type) ||
        (type.node.type === AST_NODE_TYPES.TSTypeOperator &&
          (type.node.operator === 'keyof' ||
            (type.node.operator === 'readonly' &&
              type.node.typeAnnotation &&
              aliasTypes.has(type.node.typeAnnotation.type))))
      ) {
        // alias / keyword
        checkAndReport(allowAliases!, isTopLevel, type, 'Aliases');
      } else {
        // unhandled type - shouldn't happen
        reportError(type.node, type.compositionType, isTopLevel, 'Unhandled');
      }
      /* eslint-enable @typescript-eslint/no-non-null-assertion */
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Validates the node looking for aliases, callbacks and literals.
     * @param type the type of composition this alias is part of (null if not
     *                                  part of a composition)
     * @param isTopLevel a flag indicating this is the top level node.
     */
```

- **Parameters**:
  - `type: TypeWithLabel`
  - `isTopLevel: boolean`
- **Return Type**: `void`
- **Calls**:
  - `reportError`
  - `checkAndReport`
  - `isValidTupleType`
  - `isValidGeneric`
  - `type.node.type.endsWith`
  - `aliasTypes.has`
- **Internal Comments**:
```
// https://github.com/typescript-eslint/typescript-eslint/issues/5439
/* eslint-disable @typescript-eslint/no-non-null-assertion */
// callback
// conditional type
// literal object type (x3)
// mapped type (x3)
// tuple types (x3)
// alias / keyword (x3)
// unhandled type - shouldn't happen (x3)
```

### `getTypes(node: TSESTree.Node, compositionType: CompositionType | null): TypeWithLabel[]`

<details><summary>Code</summary>

```ts
function getTypes(
      node: TSESTree.Node,
      compositionType: CompositionType | null = null,
    ): TypeWithLabel[] {
      if (
        node.type === AST_NODE_TYPES.TSUnionType ||
        node.type === AST_NODE_TYPES.TSIntersectionType
      ) {
        return node.types.flatMap(type => getTypes(type, node.type));
      }
      return [{ node, compositionType }];
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Flatten the given type into an array of its dependencies
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `compositionType: CompositionType | null`
- **Return Type**: `TypeWithLabel[]`
- **Calls**:
  - `node.types.flatMap`
  - `getTypes`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `TypeWithLabel`

<details><summary>Interface Code</summary>

```ts
interface TypeWithLabel {
  compositionType: CompositionType | null;
  node: TSESTree.Node;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `compositionType` | `CompositionType | null` | ✗ |  |
| `node` | `TSESTree.Node` | ✗ |  |


---

## Type Aliases

### `Values`

```ts
type Values = | 'always'
  | 'in-intersections'
  | 'in-unions'
  | 'in-unions-and-intersections'
  | 'never';
```

### `Options`

```ts
type Options = [
  {
    allowAliases?: Values;
    allowCallbacks?: 'always' | 'never';
    allowConditionalTypes?: 'always' | 'never';
    allowConstructors?: 'always' | 'never';
    allowGenerics?: 'always' | 'never';
    allowLiterals?: Values;
    allowMappedTypes?: Values;
    allowTupleTypes?: Values;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'noCompositionAlias' | 'noTypeAlias';
```

### `CompositionType`

```ts
type CompositionType = | AST_NODE_TYPES.TSIntersectionType
  | AST_NODE_TYPES.TSUnionType;
```


---