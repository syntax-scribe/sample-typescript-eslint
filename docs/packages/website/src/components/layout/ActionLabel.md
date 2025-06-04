[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `ActionLabel.tsx`

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
📂 **`packages/website/src/components/layout/ActionLabel.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |
| `styles` | `./InputLabel.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `button` | element | className={styles.optionLabel}, onClick={props.onClick} | <span>, {props.children} |
| `span` | element | *none* | {props.name} |


---

## Functions

### `ActionLabel(props: InputLabelProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function ActionLabel(props: InputLabelProps): React.JSX.Element {
  return (
    <button className={styles.optionLabel} onClick={props.onClick}>
      <span>{props.name}</span>
      {props.children}
    </button>
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
  readonly onClick: () => void;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `children` | `React.ReactNode` | ✗ |  |
| `name` | `string` | ✗ |  |
| `onClick` | `() => void` | ✗ |  |


---