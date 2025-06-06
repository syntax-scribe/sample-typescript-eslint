[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Text.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 💠 JSX Elements | 4 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/inputs/Text.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `SearchIcon` | `@site/src/icons/search.svg` |
| `React` | `react` |
| `styles` | `./Text.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `Fragment` | fragment | *none* | <label> |
| `label` | element | className={styles.textInput} | {props.type === 'search' && <SearchIcon />}, <input> |
| `SearchIcon` | component | *none* | *none* |
| `input` | element | autoComplete="off", className={props.className}, name={props.name}, onChange={(e): void => props.onChange(e.target.value)}, placeholder={props.placeholder}, ref={ref}, type={props.type ?? 'text'}, value={props.value} | *none* |


---

## Interfaces

### `DropdownProps`

<details><summary>Interface Code</summary>

```ts
export interface DropdownProps {
  readonly className?: string;
  readonly name: string;
  readonly onChange: (value: string) => void;
  readonly placeholder?: string;
  readonly type?: 'search' | 'text';
  readonly value: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `className` | `string` | ✓ |  |
| `name` | `string` | ✗ |  |
| `onChange` | `(value: string) => void` | ✗ |  |
| `placeholder` | `string` | ✓ |  |
| `type` | `'search' | 'text'` | ✓ |  |
| `value` | `string` | ✗ |  |


---