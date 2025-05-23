[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `json-schema.ts`

## 📚 Table of Contents

- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 15
- **Type Aliases**: 5

## 🛠️ File Location:
📂 **`packages/utils/src/json-schema.ts`**

## 📦 Imports

> No imports found in this file.


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `JSONSchema4Object`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4Object {
  [key: string]: JSONSchema4TypeExtended;
}
```
</details>

### `JSONSchema4Array`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4Array extends Array<JSONSchema4TypeExtended> {}
```
</details>

### `JSONSchema4Base`

<details><summary>Interface Code</summary>

```ts
interface JSONSchema4Base {
  /**
   * Reusable definitions that can be referenced via `$ref`
   */
  $defs?: Record<string, JSONSchema4> | undefined;

  /**
   * Path to a schema defined in `definitions`/`$defs` that will form the base
   * for this schema.
   *
   * If you are defining an "array" schema (`schema: [ ... ]`) for your rule
   * then you should prefix this with `items/0` so that the validator can find
   * your definitions.
   *
   * eg: `'#/items/0/definitions/myDef'`
   *
   * Otherwise if you are defining an "object" schema (`schema: { ... }`) for
   * your rule you can directly reference your definitions
   *
   * eg: `'#/definitions/myDef'`
   */
  $ref?: string | undefined;

  $schema?: JSONSchema4Version | undefined;

  /**
   * (AND) Must be valid against all of the sub-schemas
   */
  allOf?: JSONSchema4[] | undefined;

  /**
   * (OR) Must be valid against any of the sub-schemas
   */
  anyOf?: JSONSchema4[] | undefined;

  /**
   * The default value for the item if not present
   */
  default?: JSONSchema4TypeExtended | undefined;

  /**
   * Reusable definitions that can be referenced via `$ref`
   */
  definitions?: Record<string, JSONSchema4> | undefined;

  /**
   * This attribute is a string that provides a full description of the of
   * purpose the instance property.
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.22
   */
  description?: string | undefined;

  /**
   * The value of this property MUST be another schema which will provide
   * a base schema which the current schema will inherit from.  The
   * inheritance rules are such that any instance that is valid according
   * to the current schema MUST be valid according to the referenced
   * schema.  This MAY also be an array, in which case, the instance MUST
   * be valid for all the schemas in the array.  A schema that extends
   * another schema MAY define additional attributes, constrain existing
   * attributes, or add other constraints.
   *
   * Conceptually, the behavior of extends can be seen as validating an
   * instance against all constraints in the extending schema as well as
   * the extended schema(s).
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.26
   */
  extends?: string | string[] | undefined;

  id?: string | undefined;

  /**
   * (NOT) Must not be valid against the given schema
   */
  not?: JSONSchema4 | undefined;

  /**
   * (XOR) Must be valid against exactly one of the sub-schemas
   */
  oneOf?: JSONSchema4[] | undefined;

  /**
   * This attribute indicates if the instance must have a value, and not
   * be undefined. This is false by default, making the instance
   * optional.
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.7
   */
  required?: boolean | string[] | undefined;

  /**
   * This attribute is a string that provides a short description of the
   * instance property.
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.21
   */
  title?: string | undefined;

  /**
   * A single type, or a union of simple types
   */
  type?: JSONSchema4TypeName | JSONSchema4TypeName[] | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `$defs` | `Record<string, JSONSchema4> | undefined` | ✓ |  |
| `$ref` | `string | undefined` | ✓ |  |
| `$schema` | `JSONSchema4Version | undefined` | ✓ |  |
| `allOf` | `JSONSchema4[] | undefined` | ✓ |  |
| `anyOf` | `JSONSchema4[] | undefined` | ✓ |  |
| `default` | `JSONSchema4TypeExtended | undefined` | ✓ |  |
| `definitions` | `Record<string, JSONSchema4> | undefined` | ✓ |  |
| `description` | `string | undefined` | ✓ |  |
| `extends` | `string | string[] | undefined` | ✓ |  |
| `id` | `string | undefined` | ✓ |  |
| `not` | `JSONSchema4 | undefined` | ✓ |  |
| `oneOf` | `JSONSchema4[] | undefined` | ✓ |  |
| `required` | `boolean | string[] | undefined` | ✓ |  |
| `title` | `string | undefined` | ✓ |  |
| `type` | `JSONSchema4TypeName | JSONSchema4TypeName[] | undefined` | ✓ |  |

### `JSONSchema4RefSchema`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4RefSchema extends JSONSchema4Base {
  $ref: string;
  type?: undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `$ref` | `string` | ✗ |  |
| `type` | `undefined` | ✓ |  |

### `JSONSchema4AllOfSchema`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4AllOfSchema extends JSONSchema4Base {
  allOf: JSONSchema4[];
  type?: undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `allOf` | `JSONSchema4[]` | ✗ |  |
| `type` | `undefined` | ✓ |  |

### `JSONSchema4AnyOfSchema`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4AnyOfSchema extends JSONSchema4Base {
  anyOf: JSONSchema4[];
  type?: undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `anyOf` | `JSONSchema4[]` | ✗ |  |
| `type` | `undefined` | ✓ |  |

### `JSONSchema4OneOfSchema`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4OneOfSchema extends JSONSchema4Base {
  oneOf: JSONSchema4[];
  type?: undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `oneOf` | `JSONSchema4[]` | ✗ |  |
| `type` | `undefined` | ✓ |  |

### `JSONSchema4MultiSchema`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4MultiSchema
  extends Omit<JSONSchema4ObjectSchema, 'enum' | 'type'>,
    Omit<JSONSchema4ArraySchema, 'enum' | 'type'>,
    Omit<JSONSchema4StringSchema, 'enum' | 'type'>,
    Omit<JSONSchema4NumberSchema, 'enum' | 'type'>,
    Omit<JSONSchema4BooleanSchema, 'enum' | 'type'>,
    Omit<JSONSchema4NullSchema, 'enum' | 'type'>,
    Omit<JSONSchema4AnySchema, 'enum' | 'type'> {
  /**
   * This provides an enumeration of all possible values that are valid
   * for the instance property. This MUST be an array, and each item in
   * the array represents a possible value for the instance value. If
   * this attribute is defined, the instance value MUST be one of the
   * values in the array in order for the schema to be valid.
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.19
   */
  enum?: JSONSchema4Type[];
  type: JSONSchema4TypeName[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `enum` | `JSONSchema4Type[]` | ✓ |  |
| `type` | `JSONSchema4TypeName[]` | ✗ |  |

### `JSONSchema4ObjectSchema`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4ObjectSchema extends JSONSchema4Base {
  /**
   * This attribute defines a schema for all properties that are not
   * explicitly defined in an object type definition. If specified, the
   * value MUST be a schema or a boolean. If false is provided, no
   * additional properties are allowed beyond the properties defined in
   * the schema. The default value is an empty schema which allows any
   * value for additional properties.
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.4
   */
  additionalProperties?: boolean | JSONSchema4 | undefined;

  /**
   * The `dependencies` keyword conditionally applies a sub-schema when a given
   * property is present. This schema is applied in the same way `allOf` applies
   * schemas. Nothing is merged or extended. Both schemas apply independently.
   */
  dependencies?: Record<string, JSONSchema4 | string[]> | undefined;

  /**
   * The maximum number of properties allowed for record-style schemas
   */
  maxProperties?: number | undefined;

  /**
   * The minimum number of properties required for record-style schemas
   */
  minProperties?: number | undefined;

  /**
   * This attribute is an object that defines the schema for a set of
   * property names of an object instance. The name of each property of
   * this attribute's object is a regular expression pattern in the ECMA
   * 262/Perl 5 format, while the value is a schema. If the pattern
   * matches the name of a property on the instance object, the value of
   * the instance's property MUST be valid against the pattern name's
   * schema value.
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.3
   */
  patternProperties?: Record<string, JSONSchema4> | undefined;

  /**
   * This attribute is an object with property definitions that define the
   * valid values of instance object property values. When the instance
   * value is an object, the property values of the instance object MUST
   * conform to the property definitions in this object. In this object,
   * each property definition's value MUST be a schema, and the property's
   * name MUST be the name of the instance property that it defines.  The
   * instance property value MUST be valid according to the schema from
   * the property definition. Properties are considered unordered, the
   * order of the instance properties MAY be in any order.
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.2
   */
  properties?: Record<string, JSONSchema4> | undefined;

  type: 'object';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `additionalProperties` | `boolean | JSONSchema4 | undefined` | ✓ |  |
| `dependencies` | `Record<string, JSONSchema4 | string[]> | undefined` | ✓ |  |
| `maxProperties` | `number | undefined` | ✓ |  |
| `minProperties` | `number | undefined` | ✓ |  |
| `patternProperties` | `Record<string, JSONSchema4> | undefined` | ✓ |  |
| `properties` | `Record<string, JSONSchema4> | undefined` | ✓ |  |
| `type` | `'object'` | ✗ |  |

### `JSONSchema4ArraySchema`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4ArraySchema extends JSONSchema4Base {
  /**
   * May only be defined when "items" is defined, and is a tuple of JSONSchemas.
   *
   * This provides a definition for additional items in an array instance
   * when tuple definitions of the items is provided.  This can be false
   * to indicate additional items in the array are not allowed, or it can
   * be a schema that defines the schema of the additional items.
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.6
   */
  additionalItems?: boolean | JSONSchema4 | undefined;

  /**
   * This attribute defines the allowed items in an instance array, and
   * MUST be a schema or an array of schemas.  The default value is an
   * empty schema which allows any value for items in the instance array.
   *
   * When this attribute value is a schema and the instance value is an
   * array, then all the items in the array MUST be valid according to the
   * schema.
   *
   * When this attribute value is an array of schemas and the instance
   * value is an array, each position in the instance array MUST conform
   * to the schema in the corresponding position for this array.  This
   * called tuple typing.  When tuple typing is used, additional items are
   * allowed, disallowed, or constrained by the "additionalItems"
   * (Section 5.6) attribute using the same rules as
   * "additionalProperties" (Section 5.4) for objects.
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.5
   */
  items?: JSONSchema4 | JSONSchema4[] | undefined;

  /**
   * Defines the maximum length of an array
   */
  maxItems?: number | undefined;

  /**
   * Defines the minimum length of an array
   */
  minItems?: number | undefined;

  type: 'array';

  /**
   * Enforces that all items in the array are unique
   */
  uniqueItems?: boolean | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `additionalItems` | `boolean | JSONSchema4 | undefined` | ✓ |  |
| `items` | `JSONSchema4 | JSONSchema4[] | undefined` | ✓ |  |
| `maxItems` | `number | undefined` | ✓ |  |
| `minItems` | `number | undefined` | ✓ |  |
| `type` | `'array'` | ✗ |  |
| `uniqueItems` | `boolean | undefined` | ✓ |  |

### `JSONSchema4StringSchema`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4StringSchema extends JSONSchema4Base {
  enum?: string[] | undefined;

  /**
   * The `format` keyword allows for basic semantic identification of certain
   * kinds of string values that are commonly used.
   *
   * For example, because JSON doesn’t have a “DateTime” type, dates need to be
   * encoded as strings. `format` allows the schema author to indicate that the
   * string value should be interpreted as a date.
   *
   * ajv v6 provides a few built-in formats - all other strings will cause AJV
   * to throw during schema compilation
   */
  format?:
    | 'date'
    | 'date-time'
    | 'email'
    | 'hostname'
    | 'ipv4'
    | 'ipv6'
    | 'json-pointer'
    | 'json-pointer-uri-fragment'
    | 'regex'
    | 'relative-json-pointer'
    | 'time'
    | 'uri'
    | 'uri-reference'
    | 'uri-template'
    | 'url'
    | 'uuid'
    | undefined;

  /**
   * The maximum allowed length for the string
   */
  maxLength?: number | undefined;

  /**
   * The minimum allowed length for the string
   */
  minLength?: number | undefined;

  /**
   * The `pattern` keyword is used to restrict a string to a particular regular
   * expression. The regular expression syntax is the one defined in JavaScript
   * (ECMA 262 specifically) with Unicode support.
   *
   * When defining the regular expressions, it’s important to note that the
   * string is considered valid if the expression matches anywhere within the
   * string. For example, the regular expression "p" will match any string with
   * a p in it, such as "apple" not just a string that is simply "p". Therefore,
   * it is usually less confusing, as a matter of course, to surround the
   * regular expression in ^...$, for example, "^p$", unless there is a good
   * reason not to do so.
   */
  pattern?: string | undefined;

  type: 'string';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `enum` | `string[] | undefined` | ✓ |  |
| `format` | `| 'date'
    | 'date-time'
    | 'email'
    | 'hostname'
    | 'ipv4'
    | 'ipv6'
    | 'json-pointer'
    | 'json-pointer-uri-fragment'
    | 'regex'
    | 'relative-json-pointer'
    | 'time'
    | 'uri'
    | 'uri-reference'
    | 'uri-template'
    | 'url'
    | 'uuid'
    | undefined` | ✓ |  |
| `maxLength` | `number | undefined` | ✓ |  |
| `minLength` | `number | undefined` | ✓ |  |
| `pattern` | `string | undefined` | ✓ |  |
| `type` | `'string'` | ✗ |  |

### `JSONSchema4NumberSchema`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4NumberSchema extends JSONSchema4Base {
  /**
   * This provides an enumeration of all possible values that are valid
   * for the instance property. This MUST be an array, and each item in
   * the array represents a possible value for the instance value. If
   * this attribute is defined, the instance value MUST be one of the
   * values in the array in order for the schema to be valid.
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.19
   */
  enum?: number[] | undefined;

  /**
   * The exclusive minimum allowed value for the number
   * - `true` = `x < maximum`
   * - `false` = `x <= maximum`
   *
   * Default is `false`
   */
  exclusiveMaximum?: boolean | undefined;

  /**
   * Indicates whether or not `minimum` is the inclusive or exclusive minimum
   * - `true` = `x > minimum`
   * - `false` = `x ≥ minimum`
   *
   * Default is `false`
   */
  exclusiveMinimum?: boolean | undefined;

  /**
   * The maximum allowed value for the number
   */
  maximum?: number | undefined;

  /**
   * The minimum allowed value for the number
   */
  minimum?: number | undefined;

  /**
   * Numbers can be restricted to a multiple of a given number, using the
   * `multipleOf` keyword. It may be set to any positive number.
   */
  multipleOf?: number | undefined;

  type: 'integer' | 'number';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `enum` | `number[] | undefined` | ✓ |  |
| `exclusiveMaximum` | `boolean | undefined` | ✓ |  |
| `exclusiveMinimum` | `boolean | undefined` | ✓ |  |
| `maximum` | `number | undefined` | ✓ |  |
| `minimum` | `number | undefined` | ✓ |  |
| `multipleOf` | `number | undefined` | ✓ |  |
| `type` | `'integer' | 'number'` | ✗ |  |

### `JSONSchema4BooleanSchema`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4BooleanSchema extends JSONSchema4Base {
  /**
   * This provides an enumeration of all possible values that are valid
   * for the instance property. This MUST be an array, and each item in
   * the array represents a possible value for the instance value. If
   * this attribute is defined, the instance value MUST be one of the
   * values in the array in order for the schema to be valid.
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.19
   */
  enum?: boolean[] | undefined;

  type: 'boolean';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `enum` | `boolean[] | undefined` | ✓ |  |
| `type` | `'boolean'` | ✗ |  |

### `JSONSchema4NullSchema`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4NullSchema extends JSONSchema4Base {
  /**
   * This provides an enumeration of all possible values that are valid
   * for the instance property. This MUST be an array, and each item in
   * the array represents a possible value for the instance value. If
   * this attribute is defined, the instance value MUST be one of the
   * values in the array in order for the schema to be valid.
   *
   * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.19
   */
  enum?: null[] | undefined;

  type: 'null';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `enum` | `null[] | undefined` | ✓ |  |
| `type` | `'null'` | ✗ |  |

### `JSONSchema4AnySchema`

<details><summary>Interface Code</summary>

```ts
export interface JSONSchema4AnySchema extends JSONSchema4Base {
  type: 'any';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `'any'` | ✗ |  |


---

## Type Aliases

### `JSONSchema4TypeName`

/**
 * @see https://tools.ietf.org/html/draft-zyp-json-schema-03#section-5.1
 */

```ts
type JSONSchema4TypeName = | 'any'
  | 'array'
  | 'boolean'
  | 'integer'
  | 'null'
  | 'number'
  | 'object'
  | 'string';
```

### `JSONSchema4Type`

/**
 * @see https://tools.ietf.org/html/draft-zyp-json-schema-04#section-3.5
 */

```ts
type JSONSchema4Type = boolean | number | string | null;
```

### `JSONSchema4TypeExtended`

```ts
type JSONSchema4TypeExtended = | JSONSchema4Array
  | JSONSchema4Object
  | JSONSchema4Type;
```

### `JSONSchema4Version`

/**
 * Meta schema
 *
 * Recommended values:
 * - 'http://json-schema.org/schema#'
 * - 'http://json-schema.org/hyper-schema#'
 * - 'http://json-schema.org/draft-04/schema#'
 * - 'http://json-schema.org/draft-04/hyper-schema#'
 * - 'http://json-schema.org/draft-03/schema#'
 * - 'http://json-schema.org/draft-03/hyper-schema#'
 *
 * @see https://tools.ietf.org/html/draft-handrews-json-schema-validation-01#section-5
 */

```ts
type JSONSchema4Version = string;
```

### `JSONSchema4`

/**
 * JSON Schema V4
 * @see https://tools.ietf.org/html/draft-zyp-json-schema-04
 */

```ts
type JSONSchema4 = | JSONSchema4AllOfSchema
  | JSONSchema4AnyOfSchema
  | JSONSchema4AnySchema
  | JSONSchema4ArraySchema
  | JSONSchema4BooleanSchema
  | JSONSchema4MultiSchema
  | JSONSchema4NullSchema
  | JSONSchema4NumberSchema
  | JSONSchema4ObjectSchema
  | JSONSchema4OneOfSchema
  | JSONSchema4RefSchema
  | JSONSchema4StringSchema;
```


---