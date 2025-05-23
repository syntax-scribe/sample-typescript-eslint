[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ESQueryFilter.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/ESQueryFilter.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Selector` | `esquery` |
| `useState` | `react` |
| `React` | `react` |
| `styles` | `./ESQueryFilter.module.css` |
| `Text` | `./inputs/Text` |


---

## Functions

### `ESQueryFilter({
  defaultValue,
  onChange,
  onError,
}: ESQueryFilterProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function ESQueryFilter({
  defaultValue,
  onChange,
  onError,
}: ESQueryFilterProps): React.JSX.Element {
  const [value, setValue] = useState(defaultValue ?? '');
  const changeEvent = (value: string): void => {
    setValue(value);
    try {
      const queryParsed = window.esquery.parse(value);
      onChange(value, queryParsed);
      onError(undefined);
    } catch (e: unknown) {
      onError(e instanceof Error ? e : new Error(String(e)));
    }
  };

  return (
    <div className={styles.searchContainer}>
      <Text
        name="esquery"
        onChange={changeEvent}
        placeholder="ESQuery filter"
        type="search"
        value={value}
      />
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  defaultValue,
  onChange,
  onError,
}: ESQueryFilterProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useState (from react)`
  - `setValue`
  - `window.esquery.parse`
  - `onChange`
  - `onError`
  - `String`
### `changeEvent(value: string): void`

<details><summary>Code</summary>

```ts
(value: string): void => {
    setValue(value);
    try {
      const queryParsed = window.esquery.parse(value);
      onChange(value, queryParsed);
      onError(undefined);
    } catch (e: unknown) {
      onError(e instanceof Error ? e : new Error(String(e)));
    }
  }
```
</details>

- **Parameters**:
  - `value: string`
- **Return Type**: `void`
- **Calls**:
  - `setValue`
  - `window.esquery.parse`
  - `onChange`
  - `onError`
  - `String`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `ESQueryFilterProps`

<details><summary>Interface Code</summary>

```ts
export interface ESQueryFilterProps {
  defaultValue?: string;
  readonly onChange: (filter: string, selector: Selector) => void;
  readonly onError: (value?: Error) => void;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `defaultValue` | `string` | ✓ |  |
| `onChange` | `(filter: string, selector: Selector) => void` | ✗ |  |
| `onError` | `(value?: Error) => void` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---