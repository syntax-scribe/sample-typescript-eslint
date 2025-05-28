[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `ConfigEditor.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 🧱 Classes | 0 |
| 📦 Imports | 9 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 14 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 4 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/website/src/components/config/ConfigEditor.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `clsx` | `clsx` |
| `useCallback` | `react` |
| `useMemo` | `react` |
| `useState` | `react` |
| `React` | `react` |
| `Checkbox` | `../inputs/Checkbox` |
| `Dropdown` | `../inputs/Dropdown` |
| `Text` | `../inputs/Text` |
| `styles` | `./ConfigEditor.module.css` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `newConfig` | `{ [x: string]: unknown; }` | const | `{ ...values }` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `label` | element | className={styles.searchResult} | <span>, {item.type === 'boolean' ? (
        <Checkbox
          checked={Boolean(value)}
          indeterminate={Boolean(value) && !isDefault(value, item.defaults)}
          name={`config_${item.key}`}
          onChange={(checked): void =>
            onChange(
              item.key,
              checked ? (item.defaults?.[0] ?? true) : undefined,
            )
          }
          value={item.key}
        />
      ) : (
        item.enum && (
          <Dropdown
            name={`config_${item.key}`}
            onChange={(value): void => onChange(item.key, value)}
            options={item.enum}
            value={String(value)}
          />
        )
      )} |
| `span` | element | className={styles.searchResultDescription} | <span>, {item.label && <br />}, {item.label && <span> {item.label}</span>} |
| `span` | element | className={styles.searchResultName} | {item.key} |
| `br` | element | *none* | *none* |
| `span` | element | *none* | {item.label} |
| `Checkbox` | component | checked={Boolean(value)}, indeterminate={Boolean(value) && !isDefault(value, item.defaults)}, name={`config_${item.key}`}, onChange={(checked): void =>
            onChange(
              item.key,
              checked ? (item.defaults?.[0] ?? true) : undefined,
            )
          }, value={item.key} | *none* |
| `Dropdown` | component | name={`config_${item.key}`}, onChange={(value): void => onChange(item.key, value)}, options={item.enum}, value={String(value)} | *none* |
| `div` | element | className={clsx(
        'thin-scrollbar',
        styles.searchResultContainer,
        className,
      )} | <div>, {filteredOptions.map(group => (
        <div key={group.heading}>
          <h3 className={styles.searchResultGroup}>{group.heading}</h3>
          <div>
            {group.fields.map(item => (
              <ConfigEditorField
                item={item}
                key={item.key}
                onChange={onChange}
                value={values[item.key]}
              />
            ))}
          </div>
        </div>
      ))} |
| `div` | element | className={styles.searchBar} | <Text> |
| `Text` | component | name="config-filter", onChange={setFilter}, type="search", value={filter} | *none* |
| `div` | element | key={group.heading} | <h3>, <div> |
| `h3` | element | className={styles.searchResultGroup} | {group.heading} |
| `div` | element | *none* | {group.fields.map(item => (
              <ConfigEditorField
                item={item}
                key={item.key}
                onChange={onChange}
                value={values[item.key]}
              />
            ))} |
| `ConfigEditorField` | component | item={item}, key={item.key}, onChange={onChange}, value={values[item.key]} | *none* |


---

## Functions

### `filterConfig(options: ConfigOptionsType[], filter: string): ConfigOptionsType[]`

<details><summary>Code</summary>

```ts
function filterConfig(
  options: ConfigOptionsType[],
  filter: string,
): ConfigOptionsType[] {
  return options
    .map(group => ({
      fields: group.fields.filter(item =>
        item.key.toLowerCase().includes(filter.toLowerCase()),
      ),
      heading: group.heading,
    }))
    .filter(group => group.fields.length > 0);
}
```
</details>

- **Parameters**:
  - `options: ConfigOptionsType[]`
  - `filter: string`
- **Return Type**: `ConfigOptionsType[]`
- **Calls**:
  - `options
    .map(group => ({
      fields: group.fields.filter(item =>
        item.key.toLowerCase().includes(filter.toLowerCase()),
      ),
      heading: group.heading,
    }))
    .filter`
### `isDefault(value: unknown, defaults: unknown[]): boolean`

<details><summary>Code</summary>

```ts
function isDefault(value: unknown, defaults?: unknown[]): boolean {
  return defaults ? defaults.includes(value) : value === true;
}
```
</details>

- **Parameters**:
  - `value: unknown`
  - `defaults: unknown[]`
- **Return Type**: `boolean`
- **Calls**:
  - `defaults.includes`
### `ConfigEditorField({
  item,
  onChange,
  value,
}: ConfigEditorFieldProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function ConfigEditorField({
  item,
  onChange,
  value,
}: ConfigEditorFieldProps): React.JSX.Element {
  return (
    <label className={styles.searchResult}>
      <span className={styles.searchResultDescription}>
        <span className={styles.searchResultName}>{item.key}</span>
        {item.label && <br />}
        {item.label && <span> {item.label}</span>}
      </span>
      {item.type === 'boolean' ? (
        <Checkbox
          checked={Boolean(value)}
          indeterminate={Boolean(value) && !isDefault(value, item.defaults)}
          name={`config_${item.key}`}
          onChange={(checked): void =>
            onChange(
              item.key,
              checked ? (item.defaults?.[0] ?? true) : undefined,
            )
          }
          value={item.key}
        />
      ) : (
        item.enum && (
          <Dropdown
            name={`config_${item.key}`}
            onChange={(value): void => onChange(item.key, value)}
            options={item.enum}
            value={String(value)}
          />
        )
      )}
    </label>
  );
}
```
</details>

- **Parameters**:
  - `{
  item,
  onChange,
  value,
}: ConfigEditorFieldProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `Boolean`
  - `isDefault`
  - `onChange`
  - `String`
### `ConfigEditor({
  className,
  onChange: onChangeProp,
  options,
  values,
}: ConfigEditorProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function ConfigEditor({
  className,
  onChange: onChangeProp,
  options,
  values,
}: ConfigEditorProps): React.JSX.Element {
  const [filter, setFilter] = useState<string>('');

  const filteredOptions = useMemo(() => {
    return filterConfig(options, filter);
  }, [options, filter]);

  const onChange = useCallback(
    (name: string, value: unknown): void => {
      const newConfig = { ...values };
      if (value === '' || value == null) {
        // Filter out falsy values from the new config
        // eslint-disable-next-line @typescript-eslint/no-dynamic-delete
        delete newConfig[name];
      } else {
        newConfig[name] = value;
      }
      onChangeProp(newConfig);
    },
    [values, onChangeProp],
  );

  return (
    <div
      className={clsx(
        'thin-scrollbar',
        styles.searchResultContainer,
        className,
      )}
    >
      <div className={styles.searchBar}>
        <Text
          name="config-filter"
          onChange={setFilter}
          type="search"
          value={filter}
        />
      </div>
      {filteredOptions.map(group => (
        <div key={group.heading}>
          <h3 className={styles.searchResultGroup}>{group.heading}</h3>
          <div>
            {group.fields.map(item => (
              <ConfigEditorField
                item={item}
                key={item.key}
                onChange={onChange}
                value={values[item.key]}
              />
            ))}
          </div>
        </div>
      ))}
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  className,
  onChange: onChangeProp,
  options,
  values,
}: ConfigEditorProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useState (from react)`
  - `useMemo (from react)`
  - `filterConfig`
  - `useCallback (from react)`
  - `onChangeProp`
  - `clsx (from clsx)`
  - `filteredOptions.map`
  - `group.fields.map`
- **Internal Comments**:
```
// Filter out falsy values from the new config (x2)
// eslint-disable-next-line @typescript-eslint/no-dynamic-delete (x2)
```


---

## Interfaces

### `ConfigOptionsField`

<details><summary>Interface Code</summary>

```ts
export interface ConfigOptionsField {
  defaults?: unknown[];
  enum?: string[];
  key: string;
  label?: string;
  type: 'boolean' | 'string';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `defaults` | `unknown[]` | ✓ |  |
| `enum` | `string[]` | ✓ |  |
| `key` | `string` | ✗ |  |
| `label` | `string` | ✓ |  |
| `type` | `'boolean' | 'string'` | ✗ |  |

### `ConfigOptionsType`

<details><summary>Interface Code</summary>

```ts
export interface ConfigOptionsType {
  fields: ConfigOptionsField[];
  heading: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `fields` | `ConfigOptionsField[]` | ✗ |  |
| `heading` | `string` | ✗ |  |

### `ConfigEditorProps`

<details><summary>Interface Code</summary>

```ts
export interface ConfigEditorProps {
  readonly className?: string;
  readonly onChange: (config: ConfigEditorValues) => void;
  readonly options: ConfigOptionsType[];
  readonly values: ConfigEditorValues;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `className` | `string` | ✓ |  |
| `onChange` | `(config: ConfigEditorValues) => void` | ✗ |  |
| `options` | `ConfigOptionsType[]` | ✗ |  |
| `values` | `ConfigEditorValues` | ✗ |  |

### `ConfigEditorFieldProps`

<details><summary>Interface Code</summary>

```ts
interface ConfigEditorFieldProps {
  readonly item: ConfigOptionsField;
  readonly onChange: (name: string, value: unknown) => void;
  readonly value: unknown;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `item` | `ConfigOptionsField` | ✗ |  |
| `onChange` | `(name: string, value: unknown) => void` | ✗ |  |
| `value` | `unknown` | ✗ |  |


---

## Type Aliases

### `ConfigEditorValues`

```ts
type ConfigEditorValues = Record<string, unknown>;
```


---