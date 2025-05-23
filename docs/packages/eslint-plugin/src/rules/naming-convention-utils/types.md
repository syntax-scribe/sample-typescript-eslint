[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 16
- **Interfaces**: 4
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/naming-convention-utils/types.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `MessageIds` | `../naming-convention` |
| `Options` | `../naming-convention` |
| `IndividualAndMetaSelectorsString` | `./enums` |
| `MetaSelectors` | `./enums` |
| `Modifiers` | `./enums` |
| `ModifiersString` | `./enums` |
| `PredefinedFormats` | `./enums` |
| `PredefinedFormatsString` | `./enums` |
| `Selectors` | `./enums` |
| `SelectorsString` | `./enums` |
| `TypeModifiers` | `./enums` |
| `TypeModifiersString` | `./enums` |
| `UnderscoreOptions` | `./enums` |
| `UnderscoreOptionsString` | `./enums` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `MatchRegex`

<details><summary>Interface Code</summary>

```ts
export interface MatchRegex {
  match: boolean;
  regex: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `match` | `boolean` | ✗ |  |
| `regex` | `string` | ✗ |  |

### `Selector`

<details><summary>Interface Code</summary>

```ts
export interface Selector {
  custom?: MatchRegex;
  filter?: string | MatchRegex;
  // format options
  format: PredefinedFormatsString[] | null;
  leadingUnderscore?: UnderscoreOptionsString;
  modifiers?: ModifiersString[];
  prefix?: string[];
  // selector options
  selector:
    | IndividualAndMetaSelectorsString
    | IndividualAndMetaSelectorsString[];
  suffix?: string[];
  trailingUnderscore?: UnderscoreOptionsString;
  types?: TypeModifiersString[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `custom` | `MatchRegex` | ✓ |  |
| `filter` | `string | MatchRegex` | ✓ |  |
| `format` | `PredefinedFormatsString[] | null` | ✗ |  |
| `leadingUnderscore` | `UnderscoreOptionsString` | ✓ |  |
| `modifiers` | `ModifiersString[]` | ✓ |  |
| `prefix` | `string[]` | ✓ |  |
| `selector` | `| IndividualAndMetaSelectorsString
    | IndividualAndMetaSelectorsString[]` | ✗ |  |
| `suffix` | `string[]` | ✓ |  |
| `trailingUnderscore` | `UnderscoreOptionsString` | ✓ |  |
| `types` | `TypeModifiersString[]` | ✓ |  |

### `NormalizedMatchRegex`

<details><summary>Interface Code</summary>

```ts
export interface NormalizedMatchRegex {
  match: boolean;
  regex: RegExp;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `match` | `boolean` | ✗ |  |
| `regex` | `RegExp` | ✗ |  |

### `NormalizedSelector`

<details><summary>Interface Code</summary>

```ts
export interface NormalizedSelector {
  custom: NormalizedMatchRegex | null;
  filter: NormalizedMatchRegex | null;
  // format options
  format: PredefinedFormats[] | null;
  leadingUnderscore: UnderscoreOptions | null;
  modifiers: Modifiers[] | null;
  // calculated ordering weight based on modifiers
  modifierWeight: number;
  prefix: string[] | null;
  // selector options
  selector: MetaSelectors | Selectors;
  suffix: string[] | null;
  trailingUnderscore: UnderscoreOptions | null;
  types: TypeModifiers[] | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `custom` | `NormalizedMatchRegex | null` | ✗ |  |
| `filter` | `NormalizedMatchRegex | null` | ✗ |  |
| `format` | `PredefinedFormats[] | null` | ✗ |  |
| `leadingUnderscore` | `UnderscoreOptions | null` | ✗ |  |
| `modifiers` | `Modifiers[] | null` | ✗ |  |
| `modifierWeight` | `number` | ✗ |  |
| `prefix` | `string[] | null` | ✗ |  |
| `selector` | `MetaSelectors | Selectors` | ✗ |  |
| `suffix` | `string[] | null` | ✗ |  |
| `trailingUnderscore` | `UnderscoreOptions | null` | ✗ |  |
| `types` | `TypeModifiers[] | null` | ✗ |  |


---

## Type Aliases

### `ValidatorFunction`

```ts
type ValidatorFunction = (
  node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
  modifiers?: Set<Modifiers>,
) => void;
```

### `ParsedOptions`

```ts
type ParsedOptions = Record<SelectorsString, ValidatorFunction>;
```

### `Context`

```ts
type Context = Readonly<TSESLint.RuleContext<MessageIds, Options>>;
```


---