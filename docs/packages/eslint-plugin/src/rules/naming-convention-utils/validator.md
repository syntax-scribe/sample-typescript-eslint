[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `validator.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 8 |
| 📦 Imports | 16 |
| 📊 Variables & Constants | 16 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/naming-convention-utils/validator.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `SelectorsString` | `./enums` |
| `Context` | `./types` |
| `NormalizedSelector` | `./types` |
| `getParserServices` | `../../util` |
| `MetaSelectors` | `./enums` |
| `Modifiers` | `./enums` |
| `PredefinedFormats` | `./enums` |
| `Selectors` | `./enums` |
| `TypeModifiers` | `./enums` |
| `UnderscoreOptions` | `./enums` |
| `PredefinedFormatToCheckFunction` | `./format` |
| `isMetaSelector` | `./shared` |
| `isMethodOrPropertySelector` | `./shared` |
| `selectorTypeToMessageString` | `./shared` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `selectorType` | `Selectors` | const | `Selectors[type]` | ✗ |
| `originalName` | `any` | const | `node.type === AST_NODE_TYPES.Identifier ||
      node.type === AST_NODE_TYPES.PrivateIdentifier
        ? node.name
        : `${node.value}`` | ✗ |
| `name` | `string | null` | let/var | `originalName` | ✗ |
| `option` | `UnderscoreOptions` | const | `position === 'leading'
        ? config.leadingUnderscore
        : config.trailingUnderscore` | ✗ |
| `hasSingleUnderscore` | `() => boolean` | const | `position === 'leading'
        ? (): boolean => name.startsWith('_')
        : (): boolean => name.endsWith('_')` | ✗ |
| `trimSingleUnderscore` | `() => string` | const | `position === 'leading'
        ? (): string => name.slice(1)
        : (): string => name.slice(0, -1)` | ✗ |
| `hasDoubleUnderscore` | `() => boolean` | const | `position === 'leading'
        ? (): boolean => name.startsWith('__')
        : (): boolean => name.endsWith('__')` | ✗ |
| `trimDoubleUnderscore` | `() => string` | const | `position === 'leading'
        ? (): string => name.slice(2)
        : (): string => name.slice(0, -2)` | ✗ |
| `affixes` | `string[]` | const | `config[position]` | ✗ |
| `hasAffix` | `boolean` | const | `position === 'prefix' ? name.startsWith(affix) : name.endsWith(affix)` | ✗ |
| `trimAffix` | `() => string` | const | `position === 'prefix'
          ? (): string => name.slice(affix.length)
          : (): string => name.slice(0, -affix.length)` | ✗ |
| `custom` | `NormalizedMatchRegex` | const | `config.custom` | ✗ |
| `formats` | `PredefinedFormats[]` | const | `config.format` | ✗ |
| `checker` | `(name: string) => boolean` | const | `PredefinedFormatToCheckFunction[format]` | ✗ |
| `SelectorsAllowedToHaveTypes` | `number` | const | `Selectors.variable |
  Selectors.parameter |
  Selectors.classProperty |
  Selectors.objectLiteralProperty |
  Selectors.typeProperty |
  Selectors.parameterProperty |
  Selectors.classicAccessor` | ✗ |
| `allowedTypeString` | `string` | const | `TypeModifiers[allowedType]` | ✗ |


---

## Functions

### `createValidator(type: SelectorsString, context: Context, allConfigs: NormalizedSelector[]): (
  node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
) => void`

<details><summary>Code</summary>

```ts
export function createValidator(
  type: SelectorsString,
  context: Context,
  allConfigs: NormalizedSelector[],
): (
  node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
) => void {
  // make sure the "highest priority" configs are checked first
  const selectorType = Selectors[type];
  const configs = allConfigs
    // gather all of the applicable selectors
    .filter(
      c =>
        (c.selector & selectorType) !== 0 ||
        c.selector === MetaSelectors.default,
    )
    .sort((a, b) => {
      if (a.selector === b.selector) {
        // in the event of the same selector, order by modifier weight
        // sort descending - the type modifiers are "more important"
        return b.modifierWeight - a.modifierWeight;
      }

      const aIsMeta = isMetaSelector(a.selector);
      const bIsMeta = isMetaSelector(b.selector);

      // non-meta selectors should go ahead of meta selectors
      if (aIsMeta && !bIsMeta) {
        return 1;
      }
      if (!aIsMeta && bIsMeta) {
        return -1;
      }

      const aIsMethodOrProperty = isMethodOrPropertySelector(a.selector);
      const bIsMethodOrProperty = isMethodOrPropertySelector(b.selector);

      // for backward compatibility, method and property have higher precedence than other meta selectors
      if (aIsMethodOrProperty && !bIsMethodOrProperty) {
        return -1;
      }
      if (!aIsMethodOrProperty && bIsMethodOrProperty) {
        return 1;
      }

      // both aren't meta selectors
      // sort descending - the meta selectors are "least important"
      return b.selector - a.selector;
    });

  return (
    node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
    modifiers: Set<Modifiers> = new Set<Modifiers>(),
  ): void => {
    const originalName =
      node.type === AST_NODE_TYPES.Identifier ||
      node.type === AST_NODE_TYPES.PrivateIdentifier
        ? node.name
        : `${node.value}`;

    // return will break the loop and stop checking configs
    // it is only used when the name is known to have failed or succeeded a config.
    for (const config of configs) {
      if (config.filter?.regex.test(originalName) !== config.filter?.match) {
        // name does not match the filter
        continue;
      }

      if (config.modifiers?.some(modifier => !modifiers.has(modifier))) {
        // does not have the required modifiers
        continue;
      }

      if (!isCorrectType(node, config, context, selectorType)) {
        // is not the correct type
        continue;
      }

      let name: string | null = originalName;

      name = validateUnderscore('leading', config, name, node, originalName);
      if (name == null) {
        // fail
        return;
      }

      name = validateUnderscore('trailing', config, name, node, originalName);
      if (name == null) {
        // fail
        return;
      }

      name = validateAffix('prefix', config, name, node, originalName);
      if (name == null) {
        // fail
        return;
      }

      name = validateAffix('suffix', config, name, node, originalName);
      if (name == null) {
        // fail
        return;
      }

      if (!validateCustom(config, name, node, originalName)) {
        // fail
        return;
      }

      if (
        !validatePredefinedFormat(config, name, node, originalName, modifiers)
      ) {
        // fail
        return;
      }

      // it's valid for this config, so we don't need to check any more configs
      return;
    }
  };

  // centralizes the logic for formatting the report data
  function formatReportData({
    affixes,
    count,
    custom,
    formats,
    originalName,
    position,
    processedName,
  }: {
    affixes?: string[];
    count?: 'one' | 'two';
    custom?: NonNullable<NormalizedSelector['custom']>;
    formats?: PredefinedFormats[];
    originalName: string;
    position?: 'leading' | 'prefix' | 'suffix' | 'trailing';
    processedName?: string;
  }): Record<string, unknown> {
    return {
      affixes: affixes?.join(', '),
      count,
      formats: formats?.map(f => PredefinedFormats[f]).join(', '),
      name: originalName,
      position,
      processedName,
      regex: custom?.regex.toString(),
      regexMatch:
        custom?.match === true
          ? 'match'
          : custom?.match === false
            ? 'not match'
            : null,
      type: selectorTypeToMessageString(type),
    };
  }

  /**
   * @returns the name with the underscore removed, if it is valid according to the specified underscore option, null otherwise
   */
  function validateUnderscore(
    position: 'leading' | 'trailing',
    config: NormalizedSelector,
    name: string,
    node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
    originalName: string,
  ): string | null {
    const option =
      position === 'leading'
        ? config.leadingUnderscore
        : config.trailingUnderscore;
    if (!option) {
      return name;
    }

    const hasSingleUnderscore =
      position === 'leading'
        ? (): boolean => name.startsWith('_')
        : (): boolean => name.endsWith('_');
    const trimSingleUnderscore =
      position === 'leading'
        ? (): string => name.slice(1)
        : (): string => name.slice(0, -1);

    const hasDoubleUnderscore =
      position === 'leading'
        ? (): boolean => name.startsWith('__')
        : (): boolean => name.endsWith('__');
    const trimDoubleUnderscore =
      position === 'leading'
        ? (): string => name.slice(2)
        : (): string => name.slice(0, -2);

    switch (option) {
      // ALLOW - no conditions as the user doesn't care if it's there or not
      case UnderscoreOptions.allow: {
        if (hasSingleUnderscore()) {
          return trimSingleUnderscore();
        }

        return name;
      }

      case UnderscoreOptions.allowDouble: {
        if (hasDoubleUnderscore()) {
          return trimDoubleUnderscore();
        }

        return name;
      }

      case UnderscoreOptions.allowSingleOrDouble: {
        if (hasDoubleUnderscore()) {
          return trimDoubleUnderscore();
        }

        if (hasSingleUnderscore()) {
          return trimSingleUnderscore();
        }

        return name;
      }

      // FORBID
      case UnderscoreOptions.forbid: {
        if (hasSingleUnderscore()) {
          context.report({
            data: formatReportData({
              count: 'one',
              originalName,
              position,
            }),
            messageId: 'unexpectedUnderscore',
            node,
          });
          return null;
        }

        return name;
      }

      // REQUIRE
      case UnderscoreOptions.require: {
        if (!hasSingleUnderscore()) {
          context.report({
            data: formatReportData({
              count: 'one',
              originalName,
              position,
            }),
            messageId: 'missingUnderscore',
            node,
          });
          return null;
        }

        return trimSingleUnderscore();
      }

      case UnderscoreOptions.requireDouble: {
        if (!hasDoubleUnderscore()) {
          context.report({
            data: formatReportData({
              count: 'two',
              originalName,
              position,
            }),
            messageId: 'missingUnderscore',
            node,
          });
          return null;
        }

        return trimDoubleUnderscore();
      }
    }
  }

  /**
   * @returns the name with the affix removed, if it is valid according to the specified affix option, null otherwise
   */
  function validateAffix(
    position: 'prefix' | 'suffix',
    config: NormalizedSelector,
    name: string,
    node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
    originalName: string,
  ): string | null {
    const affixes = config[position];
    if (!affixes || affixes.length === 0) {
      return name;
    }

    for (const affix of affixes) {
      const hasAffix =
        position === 'prefix' ? name.startsWith(affix) : name.endsWith(affix);
      const trimAffix =
        position === 'prefix'
          ? (): string => name.slice(affix.length)
          : (): string => name.slice(0, -affix.length);

      if (hasAffix) {
        // matches, so trim it and return
        return trimAffix();
      }
    }

    context.report({
      data: formatReportData({
        affixes,
        originalName,
        position,
      }),
      messageId: 'missingAffix',
      node,
    });
    return null;
  }

  /**
   * @returns true if the name is valid according to the `regex` option, false otherwise
   */
  function validateCustom(
    config: NormalizedSelector,
    name: string,
    node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
    originalName: string,
  ): boolean {
    const custom = config.custom;
    if (!custom) {
      return true;
    }

    const result = custom.regex.test(name);
    if (custom.match && result) {
      return true;
    }
    if (!custom.match && !result) {
      return true;
    }

    context.report({
      data: formatReportData({
        custom,
        originalName,
      }),
      messageId: 'satisfyCustom',
      node,
    });
    return false;
  }

  /**
   * @returns true if the name is valid according to the `format` option, false otherwise
   */
  function validatePredefinedFormat(
    config: NormalizedSelector,
    name: string,
    node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
    originalName: string,
    modifiers: Set<Modifiers>,
  ): boolean {
    const formats = config.format;
    if (!formats?.length) {
      return true;
    }

    if (!modifiers.has(Modifiers.requiresQuotes)) {
      for (const format of formats) {
        const checker = PredefinedFormatToCheckFunction[format];
        if (checker(name)) {
          return true;
        }
      }
    }

    context.report({
      data: formatReportData({
        formats,
        originalName,
        processedName: name,
      }),
      messageId:
        originalName === name
          ? 'doesNotMatchFormat'
          : 'doesNotMatchFormatTrimmed',
      node,
    });
    return false;
  }
}
```
</details>

- **Parameters**:
  - `type: SelectorsString`
  - `context: Context`
  - `allConfigs: NormalizedSelector[]`
- **Return Type**: `(
  node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
) => void`
- **Calls**:
  - `allConfigs
    // gather all of the applicable selectors
    .filter(
      c =>
        (c.selector & selectorType) !== 0 ||
        c.selector === MetaSelectors.default,
    )
    .sort`
  - `isMetaSelector (from ./shared)`
  - `isMethodOrPropertySelector (from ./shared)`
  - `config.filter?.regex.test`
  - `config.modifiers?.some`
  - `modifiers.has`
  - `isCorrectType`
  - `validateUnderscore`
  - `validateAffix`
  - `validateCustom`
  - `validatePredefinedFormat`
  - `affixes?.join`
  - `formats?.map(f => PredefinedFormats[f]).join`
  - `custom?.regex.toString`
  - `selectorTypeToMessageString (from ./shared)`
  - `name.startsWith`
  - `name.endsWith`
  - `name.slice`
  - `hasSingleUnderscore`
  - `trimSingleUnderscore`
  - `hasDoubleUnderscore`
  - `trimDoubleUnderscore`
  - `context.report`
  - `formatReportData`
  - `trimAffix`
  - `custom.regex.test`
  - `checker`
- **Internal Comments**:
```
// make sure the "highest priority" configs are checked first (x2)
// in the event of the same selector, order by modifier weight
// sort descending - the type modifiers are "more important"
// non-meta selectors should go ahead of meta selectors
// for backward compatibility, method and property have higher precedence than other meta selectors
// both aren't meta selectors
// sort descending - the meta selectors are "least important"
// return will break the loop and stop checking configs
// it is only used when the name is known to have failed or succeeded a config.
// name does not match the filter
// does not have the required modifiers
// is not the correct type
// fail (x6)
// it's valid for this config, so we don't need to check any more configs
// centralizes the logic for formatting the report data
/**
   * @returns the name with the underscore removed, if it is valid according to the specified underscore option, null otherwise
   */
// ALLOW - no conditions as the user doesn't care if it's there or not
// FORBID
// REQUIRE
/**
   * @returns the name with the affix removed, if it is valid according to the specified affix option, null otherwise
   */
// matches, so trim it and return
/**
   * @returns true if the name is valid according to the `regex` option, false otherwise
   */
/**
   * @returns true if the name is valid according to the `format` option, false otherwise
   */
```

### `formatReportData({
    affixes,
    count,
    custom,
    formats,
    originalName,
    position,
    processedName,
  }: {
    affixes?: string[];
    count?: 'one' | 'two';
    custom?: NonNullable<NormalizedSelector['custom']>;
    formats?: PredefinedFormats[];
    originalName: string;
    position?: 'leading' | 'prefix' | 'suffix' | 'trailing';
    processedName?: string;
  }): Record<string, unknown>`

<details><summary>Code</summary>

```ts
function formatReportData({
    affixes,
    count,
    custom,
    formats,
    originalName,
    position,
    processedName,
  }: {
    affixes?: string[];
    count?: 'one' | 'two';
    custom?: NonNullable<NormalizedSelector['custom']>;
    formats?: PredefinedFormats[];
    originalName: string;
    position?: 'leading' | 'prefix' | 'suffix' | 'trailing';
    processedName?: string;
  }): Record<string, unknown> {
    return {
      affixes: affixes?.join(', '),
      count,
      formats: formats?.map(f => PredefinedFormats[f]).join(', '),
      name: originalName,
      position,
      processedName,
      regex: custom?.regex.toString(),
      regexMatch:
        custom?.match === true
          ? 'match'
          : custom?.match === false
            ? 'not match'
            : null,
      type: selectorTypeToMessageString(type),
    };
  }
```
</details>

- **Parameters**:
  - `{
    affixes,
    count,
    custom,
    formats,
    originalName,
    position,
    processedName,
  }: {
    affixes?: string[];
    count?: 'one' | 'two';
    custom?: NonNullable<NormalizedSelector['custom']>;
    formats?: PredefinedFormats[];
    originalName: string;
    position?: 'leading' | 'prefix' | 'suffix' | 'trailing';
    processedName?: string;
  }`
- **Return Type**: `Record<string, unknown>`
- **Calls**:
  - `affixes?.join`
  - `formats?.map(f => PredefinedFormats[f]).join`
  - `custom?.regex.toString`
  - `selectorTypeToMessageString (from ./shared)`
### `validateUnderscore(position: 'leading' | 'trailing', config: NormalizedSelector, name: string, node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier, originalName: string): string | null`

<details><summary>Code</summary>

```ts
function validateUnderscore(
    position: 'leading' | 'trailing',
    config: NormalizedSelector,
    name: string,
    node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
    originalName: string,
  ): string | null {
    const option =
      position === 'leading'
        ? config.leadingUnderscore
        : config.trailingUnderscore;
    if (!option) {
      return name;
    }

    const hasSingleUnderscore =
      position === 'leading'
        ? (): boolean => name.startsWith('_')
        : (): boolean => name.endsWith('_');
    const trimSingleUnderscore =
      position === 'leading'
        ? (): string => name.slice(1)
        : (): string => name.slice(0, -1);

    const hasDoubleUnderscore =
      position === 'leading'
        ? (): boolean => name.startsWith('__')
        : (): boolean => name.endsWith('__');
    const trimDoubleUnderscore =
      position === 'leading'
        ? (): string => name.slice(2)
        : (): string => name.slice(0, -2);

    switch (option) {
      // ALLOW - no conditions as the user doesn't care if it's there or not
      case UnderscoreOptions.allow: {
        if (hasSingleUnderscore()) {
          return trimSingleUnderscore();
        }

        return name;
      }

      case UnderscoreOptions.allowDouble: {
        if (hasDoubleUnderscore()) {
          return trimDoubleUnderscore();
        }

        return name;
      }

      case UnderscoreOptions.allowSingleOrDouble: {
        if (hasDoubleUnderscore()) {
          return trimDoubleUnderscore();
        }

        if (hasSingleUnderscore()) {
          return trimSingleUnderscore();
        }

        return name;
      }

      // FORBID
      case UnderscoreOptions.forbid: {
        if (hasSingleUnderscore()) {
          context.report({
            data: formatReportData({
              count: 'one',
              originalName,
              position,
            }),
            messageId: 'unexpectedUnderscore',
            node,
          });
          return null;
        }

        return name;
      }

      // REQUIRE
      case UnderscoreOptions.require: {
        if (!hasSingleUnderscore()) {
          context.report({
            data: formatReportData({
              count: 'one',
              originalName,
              position,
            }),
            messageId: 'missingUnderscore',
            node,
          });
          return null;
        }

        return trimSingleUnderscore();
      }

      case UnderscoreOptions.requireDouble: {
        if (!hasDoubleUnderscore()) {
          context.report({
            data: formatReportData({
              count: 'two',
              originalName,
              position,
            }),
            messageId: 'missingUnderscore',
            node,
          });
          return null;
        }

        return trimDoubleUnderscore();
      }
    }
  }
```
</details>

- **JSDoc**:
```ts
/**
   * @returns the name with the underscore removed, if it is valid according to the specified underscore option, null otherwise
   */
```

- **Parameters**:
  - `position: 'leading' | 'trailing'`
  - `config: NormalizedSelector`
  - `name: string`
  - `node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier`
  - `originalName: string`
- **Return Type**: `string | null`
- **Calls**:
  - `name.startsWith`
  - `name.endsWith`
  - `name.slice`
  - `hasSingleUnderscore`
  - `trimSingleUnderscore`
  - `hasDoubleUnderscore`
  - `trimDoubleUnderscore`
  - `context.report`
  - `formatReportData`
- **Internal Comments**:
```
// ALLOW - no conditions as the user doesn't care if it's there or not
// FORBID
// REQUIRE
```

### `validateAffix(position: 'prefix' | 'suffix', config: NormalizedSelector, name: string, node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier, originalName: string): string | null`

<details><summary>Code</summary>

```ts
function validateAffix(
    position: 'prefix' | 'suffix',
    config: NormalizedSelector,
    name: string,
    node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
    originalName: string,
  ): string | null {
    const affixes = config[position];
    if (!affixes || affixes.length === 0) {
      return name;
    }

    for (const affix of affixes) {
      const hasAffix =
        position === 'prefix' ? name.startsWith(affix) : name.endsWith(affix);
      const trimAffix =
        position === 'prefix'
          ? (): string => name.slice(affix.length)
          : (): string => name.slice(0, -affix.length);

      if (hasAffix) {
        // matches, so trim it and return
        return trimAffix();
      }
    }

    context.report({
      data: formatReportData({
        affixes,
        originalName,
        position,
      }),
      messageId: 'missingAffix',
      node,
    });
    return null;
  }
```
</details>

- **JSDoc**:
```ts
/**
   * @returns the name with the affix removed, if it is valid according to the specified affix option, null otherwise
   */
```

- **Parameters**:
  - `position: 'prefix' | 'suffix'`
  - `config: NormalizedSelector`
  - `name: string`
  - `node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier`
  - `originalName: string`
- **Return Type**: `string | null`
- **Calls**:
  - `name.startsWith`
  - `name.endsWith`
  - `name.slice`
  - `trimAffix`
  - `context.report`
  - `formatReportData`
- **Internal Comments**:
```
// matches, so trim it and return
```

### `validateCustom(config: NormalizedSelector, name: string, node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier, originalName: string): boolean`

<details><summary>Code</summary>

```ts
function validateCustom(
    config: NormalizedSelector,
    name: string,
    node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
    originalName: string,
  ): boolean {
    const custom = config.custom;
    if (!custom) {
      return true;
    }

    const result = custom.regex.test(name);
    if (custom.match && result) {
      return true;
    }
    if (!custom.match && !result) {
      return true;
    }

    context.report({
      data: formatReportData({
        custom,
        originalName,
      }),
      messageId: 'satisfyCustom',
      node,
    });
    return false;
  }
```
</details>

- **JSDoc**:
```ts
/**
   * @returns true if the name is valid according to the `regex` option, false otherwise
   */
```

- **Parameters**:
  - `config: NormalizedSelector`
  - `name: string`
  - `node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier`
  - `originalName: string`
- **Return Type**: `boolean`
- **Calls**:
  - `custom.regex.test`
  - `context.report`
  - `formatReportData`
### `validatePredefinedFormat(config: NormalizedSelector, name: string, node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier, originalName: string, modifiers: Set<Modifiers>): boolean`

<details><summary>Code</summary>

```ts
function validatePredefinedFormat(
    config: NormalizedSelector,
    name: string,
    node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
    originalName: string,
    modifiers: Set<Modifiers>,
  ): boolean {
    const formats = config.format;
    if (!formats?.length) {
      return true;
    }

    if (!modifiers.has(Modifiers.requiresQuotes)) {
      for (const format of formats) {
        const checker = PredefinedFormatToCheckFunction[format];
        if (checker(name)) {
          return true;
        }
      }
    }

    context.report({
      data: formatReportData({
        formats,
        originalName,
        processedName: name,
      }),
      messageId:
        originalName === name
          ? 'doesNotMatchFormat'
          : 'doesNotMatchFormatTrimmed',
      node,
    });
    return false;
  }
```
</details>

- **JSDoc**:
```ts
/**
   * @returns true if the name is valid according to the `format` option, false otherwise
   */
```

- **Parameters**:
  - `config: NormalizedSelector`
  - `name: string`
  - `node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier`
  - `originalName: string`
  - `modifiers: Set<Modifiers>`
- **Return Type**: `boolean`
- **Calls**:
  - `modifiers.has`
  - `checker`
  - `context.report`
  - `formatReportData`
### `isCorrectType(node: TSESTree.Node, config: NormalizedSelector, context: Context, selector: Selectors): boolean`

<details><summary>Code</summary>

```ts
function isCorrectType(
  node: TSESTree.Node,
  config: NormalizedSelector,
  context: Context,
  selector: Selectors,
): boolean {
  if (config.types == null) {
    return true;
  }

  if ((SelectorsAllowedToHaveTypes & selector) === 0) {
    return true;
  }

  const services = getParserServices(context);
  const checker = services.program.getTypeChecker();
  const type = services
    .getTypeAtLocation(node)
    // remove null and undefined from the type, as we don't care about it here
    .getNonNullableType();

  for (const allowedType of config.types) {
    switch (allowedType) {
      case TypeModifiers.array:
        if (
          isAllTypesMatch(
            type,
            t => checker.isArrayType(t) || checker.isTupleType(t),
          )
        ) {
          return true;
        }
        break;

      case TypeModifiers.function:
        if (isAllTypesMatch(type, t => t.getCallSignatures().length > 0)) {
          return true;
        }
        break;

      case TypeModifiers.boolean:
      case TypeModifiers.number:
      case TypeModifiers.string: {
        const typeString = checker.typeToString(
          // this will resolve things like true => boolean, 'a' => string and 1 => number
          checker.getWidenedType(checker.getBaseTypeOfLiteralType(type)),
        );
        const allowedTypeString = TypeModifiers[allowedType];
        if (typeString === allowedTypeString) {
          return true;
        }
        break;
      }
    }
  }

  return false;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `config: NormalizedSelector`
  - `context: Context`
  - `selector: Selectors`
- **Return Type**: `boolean`
- **Calls**:
  - `getParserServices (from ../../util)`
  - `services.program.getTypeChecker`
  - `services
    .getTypeAtLocation(node)
    // remove null and undefined from the type, as we don't care about it here
    .getNonNullableType`
  - `isAllTypesMatch`
  - `checker.isArrayType`
  - `checker.isTupleType`
  - `t.getCallSignatures`
  - `checker.typeToString`
  - `checker.getWidenedType`
  - `checker.getBaseTypeOfLiteralType`
- **Internal Comments**:
```
// this will resolve things like true => boolean, 'a' => string and 1 => number (x3)
```

### `isAllTypesMatch(type: ts.Type, cb: (type: ts.Type) => boolean): boolean`

<details><summary>Code</summary>

```ts
function isAllTypesMatch(
  type: ts.Type,
  cb: (type: ts.Type) => boolean,
): boolean {
  if (type.isUnion()) {
    return type.types.every(t => cb(t));
  }

  return cb(type);
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns `true` if the type (or all union types) in the given type return true for the callback
 */
```

- **Parameters**:
  - `type: ts.Type`
  - `cb: (type: ts.Type) => boolean`
- **Return Type**: `boolean`
- **Calls**:
  - `type.isUnion`
  - `type.types.every`
  - `cb`

---