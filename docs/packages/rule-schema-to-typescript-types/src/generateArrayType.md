[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `generateArrayType.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 12
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-schema-to-typescript-types/src/generateArrayType.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |
| `JSONSchema4ArraySchema` | `@typescript-eslint/utils/json-schema` |
| `TSUtils` | `@typescript-eslint/utils` |
| `ArrayAST` | `./types` |
| `AST` | `./types` |
| `RefMap` | `./types` |
| `TupleAST` | `./types` |
| `UnionAST` | `./types` |
| `NotSupportedError` | `./errors` |
| `UnexpectedError` | `./errors` |
| `generateType` | `./generateType` |
| `getCommentLines` | `./getCommentLines` |


---

## Functions

### `generateArrayType(schema: JSONSchema4ArraySchema, refMap: RefMap): ArrayAST | TupleAST | UnionAST`

<details><summary>Code</summary>

```ts
export function generateArrayType(
  schema: JSONSchema4ArraySchema,
  refMap: RefMap,
): ArrayAST | TupleAST | UnionAST {
  if (!schema.items) {
    // it's technically valid to declare things like {type: 'array'} -> any[]
    // but that's obviously dumb and loose so let's not even bother with it
    throw new UnexpectedError('Unexpected missing items', schema);
  }
  if (!TSUtils.isArray(schema.items) && schema.additionalItems) {
    throw new NotSupportedError(
      'singlely-typed array with additionalItems',
      schema,
    );
  }

  const commentLines = getCommentLines(schema);

  const minItems = schema.minItems ?? 0;
  const maxItems =
    schema.maxItems != null && schema.maxItems < MAX_ITEMS_TO_TUPLIZE
      ? schema.maxItems
      : -1;
  const hasMaxItems = maxItems >= 0;

  if (!TSUtils.isArray(schema.items)) {
    // While we could support `minItems` and `maxItems` with tuple types,
    // for example `[T, ...T[]]`, it harms readability for documentation purposes.
    // See https://github.com/typescript-eslint/typescript-eslint/issues/11117
    return {
      commentLines,
      elementType: generateType(schema.items, refMap),
      type: 'array',
    };
  }
  // treat as a tuple
  const items: JSONSchema4[] = schema.items;
  let spreadItemSchema: JSONSchema4 | null = null;

  if (hasMaxItems && items.length < maxItems) {
    spreadItemSchema =
      typeof schema.additionalItems === 'object'
        ? schema.additionalItems
        : { type: 'any' };
  }

  // quick validation so we generate sensible types
  if (hasMaxItems && maxItems < items.length) {
    throw new UnexpectedError(
      `maxItems (${maxItems}) is smaller than the number of items schemas provided (${items.length})`,
      schema,
    );
  }
  if (maxItems > items.length && spreadItemSchema == null) {
    throw new UnexpectedError(
      'maxItems is larger than the number of items schemas, but there was not an additionalItems schema provided',
      schema,
    );
  }

  const itemTypes = items.map(i => generateType(i, refMap));
  const spreadItem =
    spreadItemSchema == null ? null : generateType(spreadItemSchema, refMap);

  if (itemTypes.length > minItems) {
    /*
    if there are more items than the min, we return a union of tuples instead of
    using the optional element operator. This is done because it is more type-safe.

    // optional element operator
    type A = [string, string?, string?]
    const a: A = ['a', undefined, 'c'] // no error

    // union of tuples
    type B = [string] | [string, string] | [string, string, string]
    const b: B = ['a', undefined, 'c'] // TS error
    */
    const cumulativeTypesList = itemTypes.slice(0, minItems);
    const typesToUnion: AST[] = [];
    if (cumulativeTypesList.length > 0) {
      // actually has minItems, so add the initial state
      typesToUnion.push(createTupleType(cumulativeTypesList));
    } else {
      // no minItems means it's acceptable to have an empty tuple type
      typesToUnion.push(createTupleType([]));
    }

    for (let i = minItems; i < itemTypes.length; i += 1) {
      cumulativeTypesList.push(itemTypes[i]);

      if (i === itemTypes.length - 1) {
        // only the last item in the union should have the spread parameter
        typesToUnion.push(createTupleType(cumulativeTypesList, spreadItem));
      } else {
        typesToUnion.push(createTupleType(cumulativeTypesList));
      }
    }

    return {
      commentLines,
      elements: typesToUnion,
      type: 'union',
    };
  }

  return {
    commentLines,
    elements: itemTypes,
    spreadType: spreadItem,
    type: 'tuple',
  };
}
```
</details>

- **Parameters**:
  - `schema: JSONSchema4ArraySchema`
  - `refMap: RefMap`
- **Return Type**: `ArrayAST | TupleAST | UnionAST`
- **Calls**:
  - `TSUtils.isArray`
  - `getCommentLines (from ./getCommentLines)`
  - `generateType (from ./generateType)`
  - `items.map`
  - `itemTypes.slice`
  - `typesToUnion.push`
  - `createTupleType`
  - `cumulativeTypesList.push`
- **Internal Comments**:
```
// it's technically valid to declare things like {type: 'array'} -> any[]
// but that's obviously dumb and loose so let's not even bother with it
// While we could support `minItems` and `maxItems` with tuple types,
// for example `[T, ...T[]]`, it harms readability for documentation purposes.
// See https://github.com/typescript-eslint/typescript-eslint/issues/11117
// treat as a tuple (x2)
// quick validation so we generate sensible types
/*
    if there are more items than the min, we return a union of tuples instead of
    using the optional element operator. This is done because it is more type-safe.

    // optional element operator
    type A = [string, string?, string?]
    const a: A = ['a', undefined, 'c'] // no error

    // union of tuples
    type B = [string] | [string, string] | [string, string, string]
    const b: B = ['a', undefined, 'c'] // TS error
    */ (x2)
// actually has minItems, so add the initial state (x4)
// no minItems means it's acceptable to have an empty tuple type (x4)
// only the last item in the union should have the spread parameter (x4)
```

### `createTupleType(elements: AST[], spreadType: AST | null): TupleAST`

<details><summary>Code</summary>

```ts
function createTupleType(
  elements: AST[],
  spreadType: AST | null = null,
): TupleAST {
  return {
    type: 'tuple',
    // clone the array because we know we'll keep mutating it
    commentLines: [],
    elements: [...elements],
    spreadType,
  };
}
```
</details>

- **Parameters**:
  - `elements: AST[]`
  - `spreadType: AST | null`
- **Return Type**: `TupleAST`
- **Internal Comments**:
```
// clone the array because we know we'll keep mutating it (x2)
```


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