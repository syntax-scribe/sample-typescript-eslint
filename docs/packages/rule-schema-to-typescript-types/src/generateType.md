[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `generateType.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 10 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-schema-to-typescript-types/src/generateType.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |
| `TSUtils` | `@typescript-eslint/utils` |
| `AST` | `./types` |
| `RefMap` | `./types` |
| `NotSupportedError` | `./errors` |
| `UnexpectedError` | `./errors` |
| `generateArrayType` | `./generateArrayType` |
| `generateObjectType` | `./generateObjectType` |
| `generateUnionType` | `./generateUnionType` |
| `getCommentLines` | `./getCommentLines` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `UNSUPPORTED_KEYWORDS` | `Set<string>` | const | `new Set([
  'allOf',
  'dependencies',
  'extends',
  'maxProperties',
  'minProperties',
  'multipleOf',
  'not',
  'patternProperties',
])` | ✗ |


---

## Functions

### `generateType(schema: JSONSchema4, refMap: RefMap): AST`

<details><summary>Code</summary>

```ts
export function generateType(schema: JSONSchema4, refMap: RefMap): AST {
  const unsupportedProps = Object.keys(schema).filter(key =>
    UNSUPPORTED_KEYWORDS.has(key),
  );
  if (unsupportedProps.length > 0) {
    throw new NotSupportedError(unsupportedProps.join(','), schema);
  }

  const commentLines = getCommentLines(schema);

  if (schema.$ref) {
    const refName = refMap.get(schema.$ref);
    if (refName == null) {
      throw new UnexpectedError(
        `Could not find definition for $ref ${
          schema.$ref
        }.\nAvailable refs:\n${[...refMap.keys()].join('\n')})`,
        schema,
      );
    }
    return {
      commentLines,
      type: 'type-reference',
      typeName: refName,
    };
  }
  if ('enum' in schema && schema.enum) {
    return {
      ...generateUnionType(schema.enum, refMap),
      commentLines,
    };
  }
  if ('anyOf' in schema && schema.anyOf) {
    return {
      // a union isn't *TECHNICALLY* correct - technically anyOf is actually
      // anyOf: [T, U, V] -> T | U | V | T & U | T & V | U & V
      // in practice though it is most used to emulate a oneOf
      ...generateUnionType(schema.anyOf, refMap),
      commentLines,
    };
  }
  if ('oneOf' in schema && schema.oneOf) {
    return {
      ...generateUnionType(schema.oneOf, refMap),
      commentLines,
    };
  }

  if (!('type' in schema) || schema.type == null) {
    throw new NotSupportedError(
      'untyped schemas without one of [$ref, enum, oneOf]',
      schema,
    );
  }
  if (TSUtils.isArray(schema.type)) {
    throw new NotSupportedError('schemas with multiple types', schema);
  }

  switch (schema.type) {
    case 'any':
      return {
        commentLines,
        type: 'type-reference',
        typeName: 'unknown',
      };

    case 'null':
      return {
        commentLines,
        type: 'type-reference',
        typeName: 'null',
      };

    case 'number':
    case 'string':
      return {
        code: schema.type,
        commentLines,
        type: 'literal',
      };

    case 'array':
      return generateArrayType(schema, refMap);

    case 'boolean':
      return {
        commentLines,
        type: 'type-reference',
        typeName: 'boolean',
      };

    case 'integer':
      return {
        commentLines,
        type: 'type-reference',
        typeName: 'number',
      };

    case 'object':
      return generateObjectType(schema, refMap);
  }
}
```
</details>

- **Parameters**:
  - `schema: JSONSchema4`
  - `refMap: RefMap`
- **Return Type**: `AST`
- **Calls**:
  - `Object.keys(schema).filter`
  - `UNSUPPORTED_KEYWORDS.has`
  - `unsupportedProps.join`
  - `getCommentLines (from ./getCommentLines)`
  - `refMap.get`
  - `[...refMap.keys()].join`
  - `refMap.keys`
  - `generateUnionType (from ./generateUnionType)`
  - `TSUtils.isArray`
  - `generateArrayType (from ./generateArrayType)`
  - `generateObjectType (from ./generateObjectType)`
- **Internal Comments**:
```
// a union isn't *TECHNICALLY* correct - technically anyOf is actually
// anyOf: [T, U, V] -> T | U | V | T & U | T & V | U & V
// in practice though it is most used to emulate a oneOf
```


---