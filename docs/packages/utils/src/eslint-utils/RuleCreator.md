[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `RuleCreator.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 6 |
| 🔄 Re-exports | 1 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Re-exports](#re-exports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/utils/src/eslint-utils/RuleCreator.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleContext` | `../ts-eslint/Rule` |
| `RuleListener` | `../ts-eslint/Rule` |
| `RuleMetaData` | `../ts-eslint/Rule` |
| `RuleMetaDataDocs` | `../ts-eslint/Rule` |
| `RuleModule` | `../ts-eslint/Rule` |
| `applyDefault` | `./applyDefault` |


---

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| named | `../ts-eslint/Rule` | RuleListener, RuleModule |


---

## Functions

### `RuleCreator(urlCreator: (ruleName: string) => string): <Options extends readonly unknown[], MessageIds extends string>({ meta, name, ...rule }: Readonly<RuleWithMetaAndName<Options, MessageIds, PluginDocs>>) => RuleModule<...>`

<details><summary>Code</summary>

```ts
export function RuleCreator<PluginDocs = unknown>(
  urlCreator: (ruleName: string) => string,
) {
  // This function will get much easier to call when this is merged https://github.com/Microsoft/TypeScript/pull/26349
  // TODO - when the above PR lands; add type checking for the context.report `data` property
  return function createNamedRule<
    Options extends readonly unknown[],
    MessageIds extends string,
  >({
    meta,
    name,
    ...rule
  }: Readonly<
    RuleWithMetaAndName<Options, MessageIds, PluginDocs>
  >): RuleModule<MessageIds, Options, PluginDocs> {
    return createRule<Options, MessageIds, PluginDocs>({
      meta: {
        ...meta,
        docs: {
          ...meta.docs,
          url: urlCreator(name),
        },
      },
      ...rule,
    });
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Creates reusable function to create rules with default options and docs URLs.
 *
 * @param urlCreator Creates a documentation URL for a given rule name.
 * @returns Function to create a rule with the docs URL format.
 */
```

- **Parameters**:
  - `urlCreator: (ruleName: string) => string`
- **Return Type**: `<Options extends readonly unknown[], MessageIds extends string>({ meta, name, ...rule }: Readonly<RuleWithMetaAndName<Options, MessageIds, PluginDocs>>) => RuleModule<...>`
- **Calls**:
  - `createRule`
  - `urlCreator`
- **Internal Comments**:
```
// This function will get much easier to call when this is merged https://github.com/Microsoft/TypeScript/pull/26349
// TODO - when the above PR lands; add type checking for the context.report `data` property
```

### `createRule({
  create,
  defaultOptions,
  meta,
}: Readonly<RuleWithMeta<Options, MessageIds, PluginDocs>>): RuleModule<
  MessageIds,
  Options,
  PluginDocs
>`

<details><summary>Code</summary>

```ts
function createRule<
  Options extends readonly unknown[],
  MessageIds extends string,
  PluginDocs = unknown,
>({
  create,
  defaultOptions,
  meta,
}: Readonly<RuleWithMeta<Options, MessageIds, PluginDocs>>): RuleModule<
  MessageIds,
  Options,
  PluginDocs
> {
  return {
    create(context: Readonly<RuleContext<MessageIds, Options>>): RuleListener {
      const optionsWithDefault = applyDefault(defaultOptions, context.options);
      return create(context, optionsWithDefault);
    },
    defaultOptions,
    meta,
  };
}
```
</details>

- **Parameters**:
  - `{
  create,
  defaultOptions,
  meta,
}: Readonly<RuleWithMeta<Options, MessageIds, PluginDocs>>`
- **Return Type**: `RuleModule<
  MessageIds,
  Options,
  PluginDocs
>`
- **Calls**:
  - `applyDefault (from ./applyDefault)`
  - `create`

---

## Interfaces

### `RuleCreateAndOptions<Options extends readonly unknown[], MessageIds extends string>`

<details><summary>Interface Code</summary>

```ts
export interface RuleCreateAndOptions<
  Options extends readonly unknown[],
  MessageIds extends string,
> {
  create: (
    context: Readonly<RuleContext<MessageIds, Options>>,
    optionsWithDefault: Readonly<Options>,
  ) => RuleListener;
  defaultOptions: Readonly<Options>;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `create` | `(
    context: Readonly<RuleContext<MessageIds, Options>>,
    optionsWithDefault: Readonly<Options>,
  ) => RuleListener` | ✗ |  |
| `defaultOptions` | `Readonly<Options>` | ✗ |  |

### `RuleWithMeta<Options extends readonly unknown[], MessageIds extends string, Docs = unknown>`

<details><summary>Interface Code</summary>

```ts
export interface RuleWithMeta<
  Options extends readonly unknown[],
  MessageIds extends string,
  Docs = unknown,
> extends RuleCreateAndOptions<Options, MessageIds> {
  meta: RuleMetaData<MessageIds, Docs, Options>;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `meta` | `RuleMetaData<MessageIds, Docs, Options>` | ✗ |  |

### `RuleWithMetaAndName<Options extends readonly unknown[], MessageIds extends string, Docs = unknown>`

<details><summary>Interface Code</summary>

```ts
export interface RuleWithMetaAndName<
  Options extends readonly unknown[],
  MessageIds extends string,
  Docs = unknown,
> extends RuleCreateAndOptions<Options, MessageIds> {
  meta: NamedCreateRuleMeta<MessageIds, Docs, Options>;
  name: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `meta` | `NamedCreateRuleMeta<MessageIds, Docs, Options>` | ✗ |  |
| `name` | `string` | ✗ |  |


---

## Type Aliases

### `NamedCreateRuleMetaDocs`

```ts
type NamedCreateRuleMetaDocs = Omit<RuleMetaDataDocs, 'url'>;
```

### `NamedCreateRuleMeta<MessageIds extends string extends string, PluginDocs = unknown = unknown, Options extends readonly unknown[] = [] extends readonly unknown[] = []>`

```ts
type NamedCreateRuleMeta<MessageIds extends string extends string, PluginDocs = unknown = unknown, Options extends readonly unknown[] = [] extends readonly unknown[] = []> = {
  docs: PluginDocs & RuleMetaDataDocs;
} & Omit<RuleMetaData<MessageIds, PluginDocs, Options>, 'docs'>;
```


---