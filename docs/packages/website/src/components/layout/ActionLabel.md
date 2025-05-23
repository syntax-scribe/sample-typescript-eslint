[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `ActionLabel.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/layout/ActionLabel.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |
| `styles` | `./InputLabel.module.css` |


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

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---