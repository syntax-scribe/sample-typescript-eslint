[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Tooltip.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/inputs/Tooltip.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `clsx` | `clsx` |
| `React` | `react` |
| `styles` | `./Tooltip.module.css` |


---

## Functions

### `Tooltip(props: TooltipProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function Tooltip(props: TooltipProps): React.JSX.Element {
  return (
    <span
      aria-label={((props.open || props.hover) && props.text) || undefined}
      className={clsx(
        styles.tooltip,
        props.position === 'right' ? styles.tooltipRight : styles.tooltipLeft,
        props.open && styles.visible,
        props.hover && styles.hover,
      )}
    >
      {React.Children.map(props.children, child => child)}
    </span>
  );
}
```
</details>

- **Parameters**:
  - `props: TooltipProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `clsx (from clsx)`
  - `React.Children.map`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `TooltipProps`

<details><summary>Interface Code</summary>

```ts
export interface TooltipProps {
  readonly children: (false | React.JSX.Element)[] | React.JSX.Element;
  readonly hover?: boolean;
  readonly open?: boolean;
  readonly position?: 'left' | 'right';
  readonly text: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `children` | `(false | React.JSX.Element)[] | React.JSX.Element` | ✗ |  |
| `hover` | `boolean` | ✓ |  |
| `open` | `boolean` | ✓ |  |
| `position` | `'left' | 'right'` | ✓ |  |
| `text` | `string` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---