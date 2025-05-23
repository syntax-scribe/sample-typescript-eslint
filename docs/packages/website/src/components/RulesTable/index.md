[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `index.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 13
- **Classes**: 0
- **Imports**: 20
- **Interfaces**: 0
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/website/src/components/RulesTable/index.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RulesMeta` | `@site/rulesMeta` |
| `RuleRecommendation` | `@typescript-eslint/utils/ts-eslint` |
| `Link` | `@docusaurus/Link` |
| `useHistory` | `@docusaurus/router` |
| `useRulesMeta` | `@site/src/hooks/useRulesMeta` |
| `clsx` | `clsx` |
| `useMemo` | `react` |
| `React` | `react` |
| `HistorySelector` | `../../hooks/useHistorySelector` |
| `useHistorySelector` | `../../hooks/useHistorySelector` |
| `CONFIG_EMOJI` | `../constants` |
| `DEPRECATED_RULE_EMOJI` | `../constants` |
| `EXTENSION_RULE_EMOJI` | `../constants` |
| `FIXABLE_EMOJI` | `../constants` |
| `RECOMMENDED_CONFIG_EMOJI` | `../constants` |
| `STRICT_CONFIG_EMOJI` | `../constants` |
| `STYLISTIC_CONFIG_EMOJI` | `../constants` |
| `SUGGESTIONS_EMOJI` | `../constants` |
| `TYPE_INFORMATION_EMOJI` | `../constants` |
| `styles` | `./styles.module.css` |


---

## Functions

### `interpolateCode(text: string): string | (string | React.JSX.Element)[]`

<details><summary>Code</summary>

```ts
function interpolateCode(
  text: string,
): string | (string | React.JSX.Element)[] {
  const fragments = text.split(/`(.*?)`/);
  if (fragments.length === 1) {
    return text;
  }
  return fragments.map((v, i) => (i % 2 === 0 ? v : <code key={i}>{v}</code>));
}
```
</details>

- **Parameters**:
  - `text: string`
- **Return Type**: `string | (string | React.JSX.Element)[]`
- **Calls**:
  - `text.split`
  - `fragments.map`
### `getActualRecommended({
  docs,
}: RulesMeta[number]): RuleRecommendation | undefined`

<details><summary>Code</summary>

```ts
function getActualRecommended({
  docs,
}: RulesMeta[number]): RuleRecommendation | undefined {
  const recommended = docs.recommended;
  return typeof recommended === 'object' ? 'recommended' : recommended;
}
```
</details>

- **Parameters**:
  - `{
  docs,
}: RulesMeta[number]`
- **Return Type**: `RuleRecommendation | undefined`
### `RuleRow({
  rule,
}: {
  rule: RulesMeta[number];
}): React.JSX.Element | null`

<details><summary>Code</summary>

```ts
function RuleRow({
  rule,
}: {
  rule: RulesMeta[number];
}): React.JSX.Element | null {
  if (!rule.docs.url) {
    return null;
  }
  const { deprecated, fixable, hasSuggestions } = rule;
  const { extendsBaseRule, requiresTypeChecking } = rule.docs;
  const actualRecommended = getActualRecommended(rule);
  return (
    <tr>
      <td>
        <Link to={new URL(rule.docs.url).pathname}>
          <code>@typescript-eslint/{rule.name}</code>
        </Link>
        <br />
        {interpolateCode(rule.docs.description)}
      </td>
      <td className={styles.attrCol} title={actualRecommended}>
        {(() => {
          switch (actualRecommended) {
            case 'recommended':
              return RECOMMENDED_CONFIG_EMOJI;
            case 'strict':
              return STRICT_CONFIG_EMOJI;
            case 'stylistic':
              return STYLISTIC_CONFIG_EMOJI;
            default:
              // for some reason the current version of babel loader won't elide
              // this correctly recommended satisfies undefined;
              return '';
          }
        })()}
      </td>
      <td
        className={styles.attrCol}
        title={
          fixable && hasSuggestions
            ? 'fixable and has suggestions'
            : fixable
              ? 'fixable'
              : hasSuggestions
                ? 'has suggestions'
                : undefined
        }
      >
        {fixable ? FIXABLE_EMOJI : ''}
        {fixable && hasSuggestions ? <br /> : ''}
        {hasSuggestions ? SUGGESTIONS_EMOJI : ''}
      </td>
      <td
        className={styles.attrCol}
        title={requiresTypeChecking ? 'requires type information' : undefined}
      >
        {requiresTypeChecking ? TYPE_INFORMATION_EMOJI : ''}
      </td>
      <td
        className={styles.attrCol}
        title={extendsBaseRule ? 'extends base rule' : undefined}
      >
        {extendsBaseRule ? EXTENSION_RULE_EMOJI : ''}
      </td>
      <td
        className={styles.attrCol}
        title={deprecated ? 'deprecated' : undefined}
      >
        {deprecated ? DEPRECATED_RULE_EMOJI : ''}
      </td>
    </tr>
  );
}
```
</details>

- **Parameters**:
  - `{
  rule,
}: {
  rule: RulesMeta[number];
}`
- **Return Type**: `React.JSX.Element | null`
- **Calls**:
  - `getActualRecommended`
  - `interpolateCode`
  - `complex_call_1853`
- **Internal Comments**:
```
// for some reason the current version of babel loader won't elide
// this correctly recommended satisfies undefined;
```

### `RuleFilterCheckBox({
  label,
  mode,
  setMode,
}: {
  label: string;
  mode: FilterMode;
  setMode: (mode: FilterMode) => void;
}): React.JSX.Element`

<details><summary>Code</summary>

```ts
function RuleFilterCheckBox({
  label,
  mode,
  setMode,
}: {
  label: string;
  mode: FilterMode;
  setMode: (mode: FilterMode) => void;
}): React.JSX.Element {
  const toNextMode = (): void =>
    setMode(filterModes[(filterModes.indexOf(mode) + 1) % filterModes.length]);
  return (
    <li className={styles.checkboxListItem}>
      <button
        aria-label={`Toggle the filter mode. Current: ${mode}`}
        className={clsx(
          styles.checkboxLabel,
          mode === 'include' && styles.activated,
          mode === 'exclude' && styles.deactivated,
        )}
        onClick={toNextMode}
        onKeyDown={(e): void => {
          if (e.key === 'Enter') {
            toNextMode();
          }
        }}
        type="button"
      >
        <div
          aria-hidden
          className={clsx(styles.visual, styles[`visual-${mode}`])}
        />
        {label}
      </button>
    </li>
  );
}
```
</details>

- **Parameters**:
  - `{
  label,
  mode,
  setMode,
}: {
  label: string;
  mode: FilterMode;
  setMode: (mode: FilterMode) => void;
}`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `setMode`
  - `filterModes.indexOf`
  - `clsx (from clsx)`
  - `toNextMode`
### `toNextMode(): void`

<details><summary>Code</summary>

```ts
(): void =>
    setMode(filterModes[(filterModes.indexOf(mode) + 1) % filterModes.length])
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `setMode`
### `match(mode: FilterMode, value: boolean): boolean | undefined`

<details><summary>Code</summary>

```ts
function match(mode: FilterMode, value: boolean): boolean | undefined {
  if (mode === 'exclude') {
    return !value;
  }
  if (mode === 'include') {
    return value;
  }
  return undefined;
}
```
</details>

- **Parameters**:
  - `mode: FilterMode`
  - `value: boolean`
- **Return Type**: `boolean | undefined`
### `RulesTable(): React.JSX.Element`

<details><summary>Code</summary>

```ts
export default function RulesTable(): React.JSX.Element {
  const [filters, changeFilter] = useRulesFilters();

  const rules = useRulesMeta();
  const relevantRules = useMemo(
    () =>
      rules.filter(r => {
        const actualRecommended = getActualRecommended(r);
        const opinions = [
          match(filters.recommended, actualRecommended === 'recommended'),
          match(
            filters.strict,
            actualRecommended === 'recommended' ||
              actualRecommended === 'strict',
          ),
          match(filters.stylistic, actualRecommended === 'stylistic'),
          match(filters.fixable, !!r.fixable),
          match(filters.suggestions, !!r.hasSuggestions),
          match(filters.typeInformation, !!r.docs.requiresTypeChecking),
          match(filters.extension, !!r.docs.extendsBaseRule),
          match(filters.deprecated, !!r.deprecated),
        ].filter(
          (o): o is boolean =>
            // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
            o !== undefined,
        );
        return opinions.every(o => o);
      }),
    [rules, filters],
  );

  return (
    <>
      <div className={styles.checkboxListArea}>
        <em>Config Group ({CONFIG_EMOJI})</em>
        <ul className={clsx('clean-list', styles.checkboxList)}>
          <RuleFilterCheckBox
            label={`${RECOMMENDED_CONFIG_EMOJI} recommended`}
            mode={filters.recommended}
            setMode={(newMode): void => changeFilter('recommended', newMode)}
          />
          <RuleFilterCheckBox
            label={`${STRICT_CONFIG_EMOJI} strict`}
            mode={filters.strict}
            setMode={(newMode): void => changeFilter('strict', newMode)}
          />
          <RuleFilterCheckBox
            label={`${STYLISTIC_CONFIG_EMOJI} stylistic`}
            mode={filters.stylistic}
            setMode={(newMode): void => changeFilter('stylistic', newMode)}
          />
        </ul>
      </div>
      <div className={styles.checkboxListArea}>
        <em>Metadata</em>
        <ul className={clsx('clean-list', styles.checkboxList)}>
          <RuleFilterCheckBox
            label={`${FIXABLE_EMOJI} fixable`}
            mode={filters.fixable}
            setMode={(newMode): void => changeFilter('fixable', newMode)}
          />
          <RuleFilterCheckBox
            label={`${SUGGESTIONS_EMOJI} has suggestions`}
            mode={filters.suggestions}
            setMode={(newMode): void => changeFilter('suggestions', newMode)}
          />
          <RuleFilterCheckBox
            label={`${TYPE_INFORMATION_EMOJI} type checked`}
            mode={filters.typeInformation}
            setMode={(newMode): void =>
              changeFilter('typeInformation', newMode)
            }
          />
          <RuleFilterCheckBox
            label={`${EXTENSION_RULE_EMOJI} extension`}
            mode={filters.extension}
            setMode={(newMode): void => changeFilter('extension', newMode)}
          />
          <RuleFilterCheckBox
            label={`${DEPRECATED_RULE_EMOJI} deprecated`}
            mode={filters.deprecated}
            setMode={(newMode): void => changeFilter('deprecated', newMode)}
          />
        </ul>
      </div>
      <p>
        (These categories are explained in{' '}
        <a href="#filtering">more detail below</a>.)
      </p>
      <table className={styles.rulesTable}>
        <thead>
          <tr>
            <th className={styles.ruleCol}>Rule</th>
            <th className={styles.attrCol}>
              <div title="The config group that the rule belongs to, if any.">
                {CONFIG_EMOJI}
              </div>
            </th>
            <th className={styles.attrCol}>
              <div title="Whether the rule has an auto-fixer and/or has suggestions.">
                {FIXABLE_EMOJI}
              </div>
            </th>
            <th className={styles.attrCol}>
              <div title="Whether the rule requires type information from the TypeScript compiler.">
                {TYPE_INFORMATION_EMOJI}
              </div>
            </th>
            <th className={styles.attrCol}>
              <div title="Whether the rule is an extension rule (i.e. based on a core ESLint rule).">
                {EXTENSION_RULE_EMOJI}
              </div>
            </th>
            <th className={styles.attrCol}>
              <div title="Whether the rule is deprecated.">
                {DEPRECATED_RULE_EMOJI}
              </div>
            </th>
          </tr>
        </thead>
        <tbody>
          {relevantRules.map(rule => (
            <RuleRow key={rule.name} rule={rule} />
          ))}
        </tbody>
      </table>
    </>
  );
}
```
</details>

- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useRulesFilters`
  - `useRulesMeta (from @site/src/hooks/useRulesMeta)`
  - `useMemo (from react)`
  - `rules.filter`
  - `getActualRecommended`
  - `[
          match(filters.recommended, actualRecommended === 'recommended'),
          match(
            filters.strict,
            actualRecommended === 'recommended' ||
              actualRecommended === 'strict',
          ),
          match(filters.stylistic, actualRecommended === 'stylistic'),
          match(filters.fixable, !!r.fixable),
          match(filters.suggestions, !!r.hasSuggestions),
          match(filters.typeInformation, !!r.docs.requiresTypeChecking),
          match(filters.extension, !!r.docs.extendsBaseRule),
          match(filters.deprecated, !!r.deprecated),
        ].filter`
  - `match`
  - `opinions.every`
  - `clsx (from clsx)`
  - `changeFilter`
  - `relevantRules.map`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish (x2)
```

### `selectSearch(history: H.History): any`

<details><summary>Code</summary>

```ts
history =>
  history.location.search
```
</details>

- **Parameters**:
  - `history: H.History`
- **Return Type**: `any`
### `getServerSnapshot(): string`

<details><summary>Code</summary>

```ts
(): string => ''
```
</details>

- **Return Type**: `string`
### `useRulesFilters(paramsKey: string): [FiltersState, (category: FilterCategory, mode: FilterMode) => void]`

<details><summary>Code</summary>

```ts
function useRulesFilters(
  paramsKey = '',
): [FiltersState, (category: FilterCategory, mode: FilterMode) => void] {
  const history = useHistory();
  const search = useHistorySelector(selectSearch, getServerSnapshot);

  const paramValue = new URLSearchParams(search).get(paramsKey) ?? '';
  // We can't compute this in selectSearch, because we need the snapshot to be
  // comparable by value.
  const filtersState = useMemo(
    () => parseFiltersState(paramValue),
    [paramValue],
  );

  const changeFilter = (category: FilterCategory, mode: FilterMode): void => {
    const newState = { ...filtersState, [category]: mode };

    if (
      category === 'strict' &&
      mode === 'include' &&
      filtersState.recommended === 'include'
    ) {
      newState.recommended = 'exclude';
    } else if (
      category === 'recommended' &&
      mode === 'include' &&
      filtersState.strict === 'include'
    ) {
      newState.strict = 'exclude';
    }

    const searchParams = new URLSearchParams(history.location.search);
    const filtersString = stringifyFiltersState(newState);

    if (filtersString) {
      searchParams.set(paramsKey, filtersString);
    } else {
      searchParams.delete(paramsKey);
    }

    history.replace({ search: searchParams.toString() });
  };

  return [filtersState, changeFilter];
}
```
</details>

- **JSDoc**:
```ts
/**
 * @param paramsKey Optional. Whether to include rules that match the particular
 * search filter. Defaults to an empty string, which matches all rules.
 */
```

- **Parameters**:
  - `paramsKey: string`
- **Return Type**: `[FiltersState, (category: FilterCategory, mode: FilterMode) => void]`
- **Calls**:
  - `useHistory (from @docusaurus/router)`
  - `useHistorySelector (from ../../hooks/useHistorySelector)`
  - `new URLSearchParams(search).get`
  - `useMemo (from react)`
  - `parseFiltersState`
  - `stringifyFiltersState`
  - `searchParams.set`
  - `searchParams.delete`
  - `history.replace`
  - `searchParams.toString`
- **Internal Comments**:
```
// We can't compute this in selectSearch, because we need the snapshot to be (x2)
// comparable by value. (x2)
```

### `changeFilter(category: FilterCategory, mode: FilterMode): void`

<details><summary>Code</summary>

```ts
(category: FilterCategory, mode: FilterMode): void => {
    const newState = { ...filtersState, [category]: mode };

    if (
      category === 'strict' &&
      mode === 'include' &&
      filtersState.recommended === 'include'
    ) {
      newState.recommended = 'exclude';
    } else if (
      category === 'recommended' &&
      mode === 'include' &&
      filtersState.strict === 'include'
    ) {
      newState.strict = 'exclude';
    }

    const searchParams = new URLSearchParams(history.location.search);
    const filtersString = stringifyFiltersState(newState);

    if (filtersString) {
      searchParams.set(paramsKey, filtersString);
    } else {
      searchParams.delete(paramsKey);
    }

    history.replace({ search: searchParams.toString() });
  }
```
</details>

- **Parameters**:
  - `category: FilterCategory`
  - `mode: FilterMode`
- **Return Type**: `void`
- **Calls**:
  - `stringifyFiltersState`
  - `searchParams.set`
  - `searchParams.delete`
  - `history.replace`
  - `searchParams.toString`
### `stringifyFiltersState(filters: FiltersState): string`

<details><summary>Code</summary>

```ts
function stringifyFiltersState(filters: FiltersState): string {
  return Object.entries(filters)
    .map(([key, value]) =>
      value === 'include'
        ? key
        : value === 'exclude'
          ? `${NEGATION_SYMBOL}${key}`
          : '',
    )
    .filter(Boolean)
    .join('-');
}
```
</details>

- **Parameters**:
  - `filters: FiltersState`
- **Return Type**: `string`
- **Calls**:
  - `Object.entries(filters)
    .map(([key, value]) =>
      value === 'include'
        ? key
        : value === 'exclude'
          ? `${NEGATION_SYMBOL}${key}`
          : '',
    )
    .filter(Boolean)
    .join`
### `parseFiltersState(str: string): FiltersState`

<details><summary>Code</summary>

```ts
function parseFiltersState(str: string): FiltersState {
  const res: FiltersState = { ...neutralFiltersState };

  for (const part of str.split('-')) {
    const exclude = part.startsWith(NEGATION_SYMBOL);
    const key = exclude ? part.slice(1) : part;
    if (Object.hasOwn(neutralFiltersState, key)) {
      res[key as keyof typeof neutralFiltersState] = exclude
        ? 'exclude'
        : 'include';
    }
  }

  return res;
}
```
</details>

- **Parameters**:
  - `str: string`
- **Return Type**: `FiltersState`
- **Calls**:
  - `str.split`
  - `part.startsWith`
  - `part.slice`
  - `Object.hasOwn`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `FilterMode`

```ts
type FilterMode = (typeof filterModes)[number];
```

### `FilterCategory`

```ts
type FilterCategory = | 'deprecated'
  | 'extension'
  | 'fixable'
  | 'recommended'
  | 'strict'
  | 'stylistic'
  | 'suggestions'
  | 'typeInformation';
```

### `FiltersState`

```ts
type FiltersState = Record<FilterCategory, FilterMode>;
```


---