[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `schema.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 10 |
| 📊 Variables & Constants | 7 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `$DEFS` | `Record<string, JSONSchema.JSONSchema4>` | const | `{
  // enums
  predefinedFormats: {
    enum: getEnumNames(PredefinedFormats),
    type: 'string',
  },
  typeModifiers: {
    enum: getEnumNames(TypeModifiers),
    type: 'string',
  },
  underscoreOptions: {
    enum: getEnumNames(UnderscoreOptions),
    type: 'string',
  },

  // repeated types
  formatOptionsConfig: {
    oneOf: [
      {
        additionalItems: false,
        items: {
          $ref: '#/$defs/predefinedFormats',
        },
        type: 'array',
      },
      {
        type: 'null',
      },
    ],
  },
  matchRegexConfig: {
    additionalProperties: false,
    properties: {
      match: { type: 'boolean' },
      regex: { type: 'string' },
    },
    required: ['match', 'regex'],
    type: 'object',
  },
  prefixSuffixConfig: {
    additionalItems: false,
    items: {
      minLength: 1,
      type: 'string',
    },
    type: 'array',
  },
}` | ✗ |
| `UNDERSCORE_SCHEMA` | `JSONSchema.JSONSchema4` | const | `{
  $ref: '#/$defs/underscoreOptions',
}` | ✗ |
| `PREFIX_SUFFIX_SCHEMA` | `JSONSchema.JSONSchema4` | const | `{
  $ref: '#/$defs/prefixSuffixConfig',
}` | ✗ |
| `MATCH_REGEX_SCHEMA` | `JSONSchema.JSONSchema4` | const | `{
  $ref: '#/$defs/matchRegexConfig',
}` | ✗ |
| `FORMAT_OPTIONS_PROPERTIES` | `JSONSchemaProperties` | const | `{
  custom: MATCH_REGEX_SCHEMA,
  failureMessage: {
    type: 'string',
  },
  format: {
    $ref: '#/$defs/formatOptionsConfig',
  },
  leadingUnderscore: UNDERSCORE_SCHEMA,
  prefix: PREFIX_SUFFIX_SCHEMA,
  suffix: PREFIX_SUFFIX_SCHEMA,
  trailingUnderscore: UNDERSCORE_SCHEMA,
}` | ✗ |
| `selector` | `JSONSchemaProperties` | const | `{
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
  }` | ✗ |
| `SCHEMA` | `JSONSchema.JSONSchema4` | const | `{
  $defs: $DEFS,
  additionalItems: false,
  items: {
    oneOf: [
      selectorsSchema(),
      ...selectorSchema('default', false, getEnumNames(Modifiers)),

      ...selectorSchema('variableLike', false, ['unused', 'async']),
      ...selectorSchema('variable', true, [
        'const',
        'destructured',
        'exported',
        'global',
        'unused',
        'async',
      ]),
      ...selectorSchema('function', false, [
        'exported',
        'global',
        'unused',
        'async',
      ]),
      ...selectorSchema('parameter', true, ['destructured', 'unused']),

      ...selectorSchema('memberLike', false, [
        'abstract',
        'private',
        '#private',
        'protected',
        'public',
        'readonly',
        'requiresQuotes',
        'static',
        'override',
        'async',
      ]),
      ...selectorSchema('classProperty', true, [
        'abstract',
        'private',
        '#private',
        'protected',
        'public',
        'readonly',
        'requiresQuotes',
        'static',
        'override',
      ]),
      ...selectorSchema('objectLiteralProperty', true, [
        'public',
        'requiresQuotes',
      ]),
      ...selectorSchema('typeProperty', true, [
        'public',
        'readonly',
        'requiresQuotes',
      ]),
      ...selectorSchema('parameterProperty', true, [
        'private',
        'protected',
        'public',
        'readonly',
      ]),
      ...selectorSchema('property', true, [
        'abstract',
        'private',
        '#private',
        'protected',
        'public',
        'readonly',
        'requiresQuotes',
        'static',
        'override',
        'async',
      ]),

      ...selectorSchema('classMethod', false, [
        'abstract',
        'private',
        '#private',
        'protected',
        'public',
        'requiresQuotes',
        'static',
        'override',
        'async',
      ]),
      ...selectorSchema('objectLiteralMethod', false, [
        'public',
        'requiresQuotes',
        'async',
      ]),
      ...selectorSchema('typeMethod', false, ['public', 'requiresQuotes']),
      ...selectorSchema('method', false, [
        'abstract',
        'private',
        '#private',
        'protected',
        'public',
        'requiresQuotes',
        'static',
        'override',
        'async',
      ]),
      ...selectorSchema('classicAccessor', true, [
        'abstract',
        'private',
        'protected',
        'public',
        'requiresQuotes',
        'static',
        'override',
      ]),
      ...selectorSchema('autoAccessor', true, [
        'abstract',
        'private',
        'protected',
        'public',
        'requiresQuotes',
        'static',
        'override',
      ]),
      ...selectorSchema('accessor', true, [
        'abstract',
        'private',
        'protected',
        'public',
        'requiresQuotes',
        'static',
        'override',
      ]),
      ...selectorSchema('enumMember', false, ['requiresQuotes']),

      ...selectorSchema('typeLike', false, ['abstract', 'exported', 'unused']),
      ...selectorSchema('class', false, ['abstract', 'exported', 'unused']),
      ...selectorSchema('interface', false, ['exported', 'unused']),
      ...selectorSchema('typeAlias', false, ['exported', 'unused']),
      ...selectorSchema('enum', false, ['exported', 'unused']),
      ...selectorSchema('typeParameter', false, ['unused']),
      ...selectorSchema('import', false, ['default', 'namespace']),
    ],
  },
  type: 'array',
}` | ✓ |


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

## Type Aliases

### `JSONSchemaProperties`

```ts
type JSONSchemaProperties = Record<string, JSONSchema.JSONSchema4>;
```


---