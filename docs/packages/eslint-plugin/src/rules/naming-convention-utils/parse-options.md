[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `parse-options.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 13 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/naming-convention-utils/parse-options.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Context` | `./types` |
| `NormalizedSelector` | `./types` |
| `ParsedOptions` | `./types` |
| `Selector` | `./types` |
| `getEnumNames` | `../../util` |
| `MetaSelectors` | `./enums` |
| `Modifiers` | `./enums` |
| `PredefinedFormats` | `./enums` |
| `Selectors` | `./enums` |
| `TypeModifiers` | `./enums` |
| `UnderscoreOptions` | `./enums` |
| `isMetaSelector` | `./shared` |
| `createValidator` | `./validator` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `weight` | `number` | let/var | `0` | ✗ |
| `normalizedOption` | `{ custom: { match: boolean; regex: RegExp; }; filter: { match: boolean; regex: RegExp; }; format: PredefinedFormats[]; leadingUnderscore: UnderscoreOptions; ... 5 more ...; modifierWeight: number; }` | const | `{
    // format options
    custom: option.custom
      ? {
          match: option.custom.match,
          regex: new RegExp(option.custom.regex, 'u'),
        }
      : null,
    filter:
      option.filter != null
        ? typeof option.filter === 'string'
          ? {
              match: true,
              regex: new RegExp(option.filter, 'u'),
            }
          : {
              match: option.filter.match,
              regex: new RegExp(option.filter.regex, 'u'),
            }
        : null,
    format: option.format ? option.format.map(f => PredefinedFormats[f]) : null,
    leadingUnderscore:
      option.leadingUnderscore != null
        ? UnderscoreOptions[option.leadingUnderscore]
        : null,
    modifiers: option.modifiers?.map(m => Modifiers[m]) ?? null,
    prefix: option.prefix && option.prefix.length > 0 ? option.prefix : null,
    suffix: option.suffix && option.suffix.length > 0 ? option.suffix : null,
    trailingUnderscore:
      option.trailingUnderscore != null
        ? UnderscoreOptions[option.trailingUnderscore]
        : null,
    types: option.types?.map(m => TypeModifiers[m]) ?? null,
    // calculated ordering weight based on modifiers
    modifierWeight: weight,
  }` | ✗ |
| `selectors` | `IndividualAndMetaSelectorsString[]` | const | `Array.isArray(option.selector)
    ? option.selector
    : [option.selector]` | ✗ |


---

## Functions

### `normalizeOption(option: Selector): NormalizedSelector[]`

<details><summary>Code</summary>

```ts
function normalizeOption(option: Selector): NormalizedSelector[] {
  let weight = 0;
  option.modifiers?.forEach(mod => {
    weight |= Modifiers[mod];
  });
  option.types?.forEach(mod => {
    weight |= TypeModifiers[mod];
  });

  // give selectors with a filter the _highest_ priority
  if (option.filter) {
    weight |= 1 << 30;
  }

  const normalizedOption = {
    // format options
    custom: option.custom
      ? {
          match: option.custom.match,
          regex: new RegExp(option.custom.regex, 'u'),
        }
      : null,
    filter:
      option.filter != null
        ? typeof option.filter === 'string'
          ? {
              match: true,
              regex: new RegExp(option.filter, 'u'),
            }
          : {
              match: option.filter.match,
              regex: new RegExp(option.filter.regex, 'u'),
            }
        : null,
    format: option.format ? option.format.map(f => PredefinedFormats[f]) : null,
    leadingUnderscore:
      option.leadingUnderscore != null
        ? UnderscoreOptions[option.leadingUnderscore]
        : null,
    modifiers: option.modifiers?.map(m => Modifiers[m]) ?? null,
    prefix: option.prefix && option.prefix.length > 0 ? option.prefix : null,
    suffix: option.suffix && option.suffix.length > 0 ? option.suffix : null,
    trailingUnderscore:
      option.trailingUnderscore != null
        ? UnderscoreOptions[option.trailingUnderscore]
        : null,
    types: option.types?.map(m => TypeModifiers[m]) ?? null,
    // calculated ordering weight based on modifiers
    modifierWeight: weight,
  };

  const selectors = Array.isArray(option.selector)
    ? option.selector
    : [option.selector];

  return selectors.map(selector => ({
    selector: isMetaSelector(selector)
      ? MetaSelectors[selector]
      : Selectors[selector],
    ...normalizedOption,
  }));
}
```
</details>

- **Parameters**:
  - `option: Selector`
- **Return Type**: `NormalizedSelector[]`
- **Calls**:
  - `option.modifiers?.forEach`
  - `option.types?.forEach`
  - `option.format.map`
  - `option.modifiers?.map`
  - `option.types?.map`
  - `Array.isArray`
  - `selectors.map`
  - `isMetaSelector (from ./shared)`
- **Internal Comments**:
```
// give selectors with a filter the _highest_ priority
// format options (x2)
// calculated ordering weight based on modifiers (x2)
```

### `parseOptions(context: Context): ParsedOptions`

<details><summary>Code</summary>

```ts
export function parseOptions(context: Context): ParsedOptions {
  const normalizedOptions = context.options.flatMap(normalizeOption);

  return Object.fromEntries(
    getEnumNames(Selectors).map(k => [
      k,
      createValidator(k, context, normalizedOptions),
    ]),
  ) as ParsedOptions;
}
```
</details>

- **Parameters**:
  - `context: Context`
- **Return Type**: `ParsedOptions`
- **Calls**:
  - `context.options.flatMap`
  - `Object.fromEntries`
  - `getEnumNames(Selectors).map`
  - `createValidator (from ./validator)`

---