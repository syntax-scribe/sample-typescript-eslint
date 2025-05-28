[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Dropdown.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 2 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/inputs/Dropdown.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `clsx` | `clsx` |
| `React` | `react` |
| `styles` | `./Dropdown.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `select` | element | className={clsx(styles.dropdown, props.className)}, disabled={props.disabled}, name={props.name}, onChange={(e): void => {
        const selected = options.find(
          item => String(item.value) === e.target.value,
        );
        if (selected) {
          props.onChange(selected.value);
        }
      }}, value={String(props.value)} | {options.map(item => (
        <option key={String(item.value)} value={String(item.value)}>
          {item.label}
        </option>
      ))} |
| `option` | element | key={String(item.value)}, value={String(item.value)} | {item.label} |


---

## Functions

### `Dropdown(props: DropdownProps<T>): React.JSX.Element`

<details><summary>Code</summary>

```ts
function Dropdown<T extends boolean | number | string>(
  props: DropdownProps<T>,
): React.JSX.Element {
  const options: DropdownOption<T>[] = props.options.map(option =>
    typeof option !== 'object'
      ? { label: String(option), value: option }
      : option,
  );

  return (
    <select
      className={clsx(styles.dropdown, props.className)}
      disabled={props.disabled}
      name={props.name}
      onChange={(e): void => {
        const selected = options.find(
          item => String(item.value) === e.target.value,
        );
        if (selected) {
          props.onChange(selected.value);
        }
      }}
      value={String(props.value)}
    >
      {options.map(item => (
        <option key={String(item.value)} value={String(item.value)}>
          {item.label}
        </option>
      ))}
    </select>
  );
}
```
</details>

- **Parameters**:
  - `props: DropdownProps<T>`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `props.options.map`
  - `String`
  - `clsx (from clsx)`
  - `options.find`
  - `props.onChange`
  - `options.map`

---

## Interfaces

### `DropdownOption<T>`

<details><summary>Interface Code</summary>

```ts
export interface DropdownOption<T> {
  readonly label: string;
  readonly value: T;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `label` | `string` | ✗ |  |
| `value` | `T` | ✗ |  |

### `DropdownProps<T>`

<details><summary>Interface Code</summary>

```ts
export interface DropdownProps<T> {
  readonly className?: string;
  readonly disabled?: boolean;
  readonly name: string;
  readonly onChange: (value: T) => void;
  readonly options: readonly (DropdownOption<T> | T)[];
  readonly value: T | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `className` | `string` | ✓ |  |
| `disabled` | `boolean` | ✓ |  |
| `name` | `string` | ✗ |  |
| `onChange` | `(value: T) => void` | ✗ |  |
| `options` | `readonly (DropdownOption<T> | T)[]` | ✗ |  |
| `value` | `T | undefined` | ✗ |  |


---