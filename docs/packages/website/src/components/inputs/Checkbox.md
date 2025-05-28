[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Checkbox.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 1 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/inputs/Checkbox.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useCallback` | `react` |
| `React` | `react` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `input` | element | checked={props.checked && !props.indeterminate}, className={props.className}, name={props.name}, onChange={(e): void =>
        props.onChange(e.target.checked, props.value ?? '')
      }, ref={checkboxRef}, type="checkbox" | *none* |


---

## Functions

### `Checkbox(props: CheckboxProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function Checkbox(props: CheckboxProps): React.JSX.Element {
  const { indeterminate } = props;

  const checkboxRef = useCallback(
    (node: HTMLInputElement | null) => {
      if (!node) {
        return;
      }

      node.indeterminate = indeterminate ?? false;
    },
    [indeterminate],
  );

  return (
    <input
      checked={props.checked && !props.indeterminate}
      className={props.className}
      name={props.name}
      onChange={(e): void =>
        props.onChange(e.target.checked, props.value ?? '')
      }
      ref={checkboxRef}
      type="checkbox"
    />
  );
}
```
</details>

- **Parameters**:
  - `props: CheckboxProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useCallback (from react)`
  - `props.onChange`

---

## Interfaces

### `CheckboxProps`

<details><summary>Interface Code</summary>

```ts
export interface CheckboxProps {
  readonly checked: boolean | undefined;
  readonly className?: string;
  readonly indeterminate?: boolean;
  readonly name: string;
  readonly onChange: (checked: boolean, value: string) => void;
  readonly value?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `checked` | `boolean | undefined` | ✗ |  |
| `className` | `string` | ✓ |  |
| `indeterminate` | `boolean` | ✓ |  |
| `name` | `string` | ✗ |  |
| `onChange` | `(checked: boolean, value: string) => void` | ✗ |  |
| `value` | `string` | ✓ |  |


---