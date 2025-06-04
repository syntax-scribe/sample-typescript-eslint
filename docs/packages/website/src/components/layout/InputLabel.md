[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `InputLabel.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |
| 💠 JSX Elements | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/layout/InputLabel.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |
| `styles` | `./InputLabel.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `label` | element | className={styles.optionLabel} | <span>, {props.children} |
| `span` | element | *none* | {props.name} |


---

## Functions

### `InputLabel(props: InputLabelProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function InputLabel(props: InputLabelProps): React.JSX.Element {
  return (
    <label className={styles.optionLabel}>
      <span>{props.name}</span>
      {props.children}
    </label>
  );
}
```
</details>

- **Parameters**:
  - `props: InputLabelProps`
- **Return Type**: `React.JSX.Element`

---

## Interfaces

### `InputLabelProps`

<details><summary>Interface Code</summary>

```ts
export interface InputLabelProps {
  readonly children: React.ReactNode;
  readonly name: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `children` | `React.ReactNode` | ✗ |  |
| `name` | `string` | ✗ |  |


---