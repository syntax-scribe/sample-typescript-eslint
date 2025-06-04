[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `enums.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 7 |
| 🎯 Enums | 6 |


## 📚 Table of Contents

- [Type Aliases](#type-aliases)
- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/naming-convention-utils/enums.ts`**

## Type Aliases

### `PredefinedFormatsString`

```ts
type PredefinedFormatsString = keyof typeof PredefinedFormats;
```

### `UnderscoreOptionsString`

```ts
type UnderscoreOptionsString = keyof typeof UnderscoreOptions;
```

### `SelectorsString`

```ts
type SelectorsString = keyof typeof Selectors;
```

### `MetaSelectorsString`

```ts
type MetaSelectorsString = keyof typeof MetaSelectors;
```

### `IndividualAndMetaSelectorsString`

```ts
type IndividualAndMetaSelectorsString = | MetaSelectorsString
  | SelectorsString;
```

### `ModifiersString`

```ts
type ModifiersString = keyof typeof Modifiers;
```

### `TypeModifiersString`

```ts
type TypeModifiersString = keyof typeof TypeModifiers;
```


---

## Enums

### `enum PredefinedFormats`

<details><summary>Enum Code</summary>

```ts
export enum PredefinedFormats {
  camelCase = 1,
  strictCamelCase,
  PascalCase,
  StrictPascalCase,
  snake_case,
  UPPER_CASE,
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `camelCase` | `1` |  |
| `strictCamelCase` | *auto* |  |
| `PascalCase` | *auto* |  |
| `StrictPascalCase` | *auto* |  |
| `snake_case` | *auto* |  |
| `UPPER_CASE` | *auto* |  |

### `enum UnderscoreOptions`

<details><summary>Enum Code</summary>

```ts
export enum UnderscoreOptions {
  forbid = 1,
  allow,
  require,

  // special cases as it's common practice to use double underscore
  requireDouble,
  allowDouble,
  allowSingleOrDouble,
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `forbid` | `1` |  |
| `allow` | *auto* |  |
| `require` | *auto* |  |
| `requireDouble` | *auto* |  |
| `allowDouble` | *auto* |  |
| `allowSingleOrDouble` | *auto* |  |

### `enum Selectors`

<details><summary>Enum Code</summary>

```ts
export enum Selectors {
  // variableLike
  variable = 1 << 0,
  function = 1 << 1,
  parameter = 1 << 2,

  // memberLike
  parameterProperty = 1 << 3,
  classicAccessor = 1 << 4,
  enumMember = 1 << 5,
  classMethod = 1 << 6,
  objectLiteralMethod = 1 << 7,
  typeMethod = 1 << 8,
  classProperty = 1 << 9,
  objectLiteralProperty = 1 << 10,
  typeProperty = 1 << 11,
  autoAccessor = 1 << 12,

  // typeLike
  class = 1 << 13,
  interface = 1 << 14,
  typeAlias = 1 << 15,
  enum = 1 << 16,
  typeParameter = 1 << 17,

  // other
  import = 1 << 18,
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `variable` | `1 << 0` |  |
| `function` | `1 << 1` |  |
| `parameter` | `1 << 2` |  |
| `parameterProperty` | `1 << 3` |  |
| `classicAccessor` | `1 << 4` |  |
| `enumMember` | `1 << 5` |  |
| `classMethod` | `1 << 6` |  |
| `objectLiteralMethod` | `1 << 7` |  |
| `typeMethod` | `1 << 8` |  |
| `classProperty` | `1 << 9` |  |
| `objectLiteralProperty` | `1 << 10` |  |
| `typeProperty` | `1 << 11` |  |
| `autoAccessor` | `1 << 12` |  |
| `class` | `1 << 13` |  |
| `interface` | `1 << 14` |  |
| `typeAlias` | `1 << 15` |  |
| `enum` | `1 << 16` |  |
| `typeParameter` | `1 << 17` |  |
| `import` | `1 << 18` |  |

### `enum MetaSelectors`

<details><summary>Enum Code</summary>

```ts
export enum MetaSelectors {
  /* eslint-disable @typescript-eslint/prefer-literal-enum-member */
  default = -1,
  variableLike = 0 |
    Selectors.variable |
    Selectors.function |
    Selectors.parameter,
  memberLike = 0 |
    Selectors.classProperty |
    Selectors.objectLiteralProperty |
    Selectors.typeProperty |
    Selectors.parameterProperty |
    Selectors.enumMember |
    Selectors.classMethod |
    Selectors.objectLiteralMethod |
    Selectors.typeMethod |
    Selectors.classicAccessor |
    Selectors.autoAccessor,
  typeLike = 0 |
    Selectors.class |
    Selectors.interface |
    Selectors.typeAlias |
    Selectors.enum |
    Selectors.typeParameter,
  method = 0 |
    Selectors.classMethod |
    Selectors.objectLiteralMethod |
    Selectors.typeMethod,
  property = 0 |
    Selectors.classProperty |
    Selectors.objectLiteralProperty |
    Selectors.typeProperty,
  accessor = 0 | Selectors.classicAccessor | Selectors.autoAccessor,
  /* eslint-enable @typescript-eslint/prefer-literal-enum-member */
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `default` | `-1` |  |
| `variableLike` | `0 |
    Selectors.variable |
    Selectors.function |
    Selectors.parameter` |  |
| `memberLike` | `0 |
    Selectors.classProperty |
    Selectors.objectLiteralProperty |
    Selectors.typeProperty |
    Selectors.parameterProperty |
    Selectors.enumMember |
    Selectors.classMethod |
    Selectors.objectLiteralMethod |
    Selectors.typeMethod |
    Selectors.classicAccessor |
    Selectors.autoAccessor` |  |
| `typeLike` | `0 |
    Selectors.class |
    Selectors.interface |
    Selectors.typeAlias |
    Selectors.enum |
    Selectors.typeParameter` |  |
| `method` | `0 |
    Selectors.classMethod |
    Selectors.objectLiteralMethod |
    Selectors.typeMethod` |  |
| `property` | `0 |
    Selectors.classProperty |
    Selectors.objectLiteralProperty |
    Selectors.typeProperty` |  |
| `accessor` | `0 | Selectors.classicAccessor | Selectors.autoAccessor` |  |

### `enum Modifiers`

<details><summary>Enum Code</summary>

```ts
export enum Modifiers {
  // const variable
  const = 1 << 0,
  // readonly members
  readonly = 1 << 1,
  // static members
  static = 1 << 2,
  // member accessibility
  public = 1 << 3,
  protected = 1 << 4,
  private = 1 << 5,
  '#private' = 1 << 6,
  abstract = 1 << 7,
  // destructured variable
  destructured = 1 << 8,
  // variables declared in the top-level scope
  global = 1 << 9,
  // things that are exported
  exported = 1 << 10,
  // things that are unused
  unused = 1 << 11,
  // properties that require quoting
  requiresQuotes = 1 << 12,
  // class members that are overridden
  override = 1 << 13,
  // class methods, object function properties, or functions that are async via the `async` keyword
  async = 1 << 14,
  // default imports
  default = 1 << 15,
  // namespace imports
  namespace = 1 << 16,

  // make sure TypeModifiers starts at Modifiers + 1 or else sorting won't work
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `const` | `1 << 0` |  |
| `readonly` | `1 << 1` |  |
| `static` | `1 << 2` |  |
| `public` | `1 << 3` |  |
| `protected` | `1 << 4` |  |
| `private` | `1 << 5` |  |
| `'#private'` | `1 << 6` |  |
| `abstract` | `1 << 7` |  |
| `destructured` | `1 << 8` |  |
| `global` | `1 << 9` |  |
| `exported` | `1 << 10` |  |
| `unused` | `1 << 11` |  |
| `requiresQuotes` | `1 << 12` |  |
| `override` | `1 << 13` |  |
| `async` | `1 << 14` |  |
| `default` | `1 << 15` |  |
| `namespace` | `1 << 16` |  |

### `enum TypeModifiers`

<details><summary>Enum Code</summary>

```ts
export enum TypeModifiers {
  boolean = 1 << 17,
  string = 1 << 18,
  number = 1 << 19,
  function = 1 << 20,
  array = 1 << 21,
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `boolean` | `1 << 17` |  |
| `string` | `1 << 18` |  |
| `number` | `1 << 19` |  |
| `function` | `1 << 20` |  |
| `array` | `1 << 21` |  |


---