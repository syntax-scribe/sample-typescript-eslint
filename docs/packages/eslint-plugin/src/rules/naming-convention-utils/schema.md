[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `schema.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 10
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/naming-convention-utils/schema.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema` | `@typescript-eslint/utils` |
| `IndividualAndMetaSelectorsString` | `./enums` |
| `ModifiersString` | `./enums` |
| `getEnumNames` | `../../util` |
| `MetaSelectors` | `./enums` |
| `Modifiers` | `./enums` |
| `PredefinedFormats` | `./enums` |
| `Selectors` | `./enums` |
| `TypeModifiers` | `./enums` |
| `UnderscoreOptions` | `./enums` |


---

## Functions

### `selectorSchema(selectorString: IndividualAndMetaSelectorsString, allowType: boolean, modifiers: ModifiersString[]): JSONSchema.JSONSchema4[]`

<details><summary>Code</summary>

```ts
function selectorSchema(
  selectorString: IndividualAndMetaSelectorsString,
  allowType: boolean,
  modifiers?: ModifiersString[],
): JSONSchema.JSONSchema4[] {
  const selector: JSONSchemaProperties = {
    filter: {
      oneOf: [
        {
          minLength: 1,
          type: 'string',
        },
        MATCH_REGEX_SCHEMA,
      ],
    },
    selector: {
      enum: [selectorString],
      type: 'string',
    },
  };
  if (modifiers && modifiers.length > 0) {
    selector.modifiers = {
      additionalItems: false,
      items: {
        enum: modifiers,
        type: 'string',
      },
      type: 'array',
    };
  }
  if (allowType) {
    selector.types = {
      additionalItems: false,
      items: {
        $ref: '#/$defs/typeModifiers',
      },
      type: 'array',
    };
  }

  return [
    {
      additionalProperties: false,
      description: `Selector '${selectorString}'`,
      properties: {
        ...FORMAT_OPTIONS_PROPERTIES,
        ...selector,
      },
      required: ['selector', 'format'],
      type: 'object',
    },
  ];
}
```
</details>

- **Parameters**:
  - `selectorString: IndividualAndMetaSelectorsString`
  - `allowType: boolean`
  - `modifiers: ModifiersString[]`
- **Return Type**: `JSONSchema.JSONSchema4[]`
### `selectorsSchema(): JSONSchema.JSONSchema4`

<details><summary>Code</summary>

```ts
function selectorsSchema(): JSONSchema.JSONSchema4 {
  return {
    additionalProperties: false,
    description: 'Multiple selectors in one config',
    properties: {
      ...FORMAT_OPTIONS_PROPERTIES,
      filter: {
        oneOf: [
          {
            minLength: 1,
            type: 'string',
          },
          MATCH_REGEX_SCHEMA,
        ],
      },
      modifiers: {
        additionalItems: false,
        items: {
          enum: getEnumNames(Modifiers),
          type: 'string',
        },
        type: 'array',
      },
      selector: {
        additionalItems: false,
        items: {
          enum: [...getEnumNames(MetaSelectors), ...getEnumNames(Selectors)],
          type: 'string',
        },
        type: 'array',
      },
      types: {
        additionalItems: false,
        items: {
          $ref: '#/$defs/typeModifiers',
        },
        type: 'array',
      },
    },
    required: ['selector', 'format'],
    type: 'object',
  };
}
```
</details>

- **Return Type**: `JSONSchema.JSONSchema4`
- **Calls**:
  - `getEnumNames (from ../../util)`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `JSONSchemaProperties`

```ts
type JSONSchemaProperties = Record<string, JSONSchema.JSONSchema4>;
```


---