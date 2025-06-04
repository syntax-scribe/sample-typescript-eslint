[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `generateObjectType.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-schema-to-typescript-types/src/generateObjectType.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema4ObjectSchema` | `@typescript-eslint/utils/json-schema` |
| `requiresQuoting` | `@typescript-eslint/type-utils` |
| `TSUtils` | `@typescript-eslint/utils` |
| `AST` | `./types` |
| `ObjectAST` | `./types` |
| `RefMap` | `./types` |
| `generateType` | `./generateType` |
| `getCommentLines` | `./getCommentLines` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `indexSignature` | `AST | null` | let/var | `null` | ✗ |
| `properties` | `ObjectAST['properties']` | const | `[]` | ✗ |
| `required` | `Set<unknown>` | const | `new Set(
    TSUtils.isArray(schema.required) ? schema.required : [],
  )` | ✗ |
| `sanitisedPropName` | `string` | const | `requiresQuoting(propName)
        ? `'${propName}'`
        : propName` | ✗ |


---

## Functions

### `generateObjectType(schema: JSONSchema4ObjectSchema, refMap: RefMap): ObjectAST`

<details><summary>Code</summary>

```ts
export function generateObjectType(
  schema: JSONSchema4ObjectSchema,
  refMap: RefMap,
): ObjectAST {
  const commentLines = getCommentLines(schema);

  let indexSignature: AST | null = null;
  if (
    schema.additionalProperties === true ||
    // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
    schema.additionalProperties === undefined
  ) {
    indexSignature = {
      commentLines: [],
      type: 'type-reference',
      typeName: 'unknown',
    };
  } else if (typeof schema.additionalProperties === 'object') {
    const indexSigType = generateType(schema.additionalProperties, refMap);
    indexSignature = indexSigType;
  }

  const properties: ObjectAST['properties'] = [];
  const required = new Set(
    TSUtils.isArray(schema.required) ? schema.required : [],
  );
  if (schema.properties) {
    const propertyDefs = Object.entries(schema.properties);
    for (const [propName, propSchema] of propertyDefs) {
      const propType = generateType(propSchema, refMap);
      const sanitisedPropName = requiresQuoting(propName)
        ? `'${propName}'`
        : propName;
      properties.push({
        name: sanitisedPropName,
        optional: !required.has(propName),
        type: propType,
      });
    }
  }

  return {
    commentLines,
    indexSignature,
    properties,
    type: 'object',
  };
}
```
</details>

- **Parameters**:
  - `schema: JSONSchema4ObjectSchema`
  - `refMap: RefMap`
- **Return Type**: `ObjectAST`
- **Calls**:
  - `getCommentLines (from ./getCommentLines)`
  - `generateType (from ./generateType)`
  - `TSUtils.isArray`
  - `Object.entries`
  - `requiresQuoting (from @typescript-eslint/type-utils)`
  - `properties.push`
  - `required.has`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish (x3)
```


---