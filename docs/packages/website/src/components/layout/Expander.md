[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Expander.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/layout/Expander.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Collapsible` | `@docusaurus/theme-common` |
| `useCollapsible` | `@docusaurus/theme-common` |
| `ArrowIcon` | `@site/src/icons/arrow.svg` |
| `clsx` | `clsx` |
| `React` | `react` |
| `styles` | `./Expander.module.css` |


---

## Functions

### `Expander(props: ExpanderProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function Expander(props: ExpanderProps): React.JSX.Element {
  const { collapsed, toggleCollapsed } = useCollapsible({
    initialState: false,
  });

  return (
    <div className={clsx(styles.expander, props.className)}>
      <button className={styles.heading} onClick={toggleCollapsed}>
        <ArrowIcon
          className={clsx(styles.arrow, !collapsed && styles.expandedArrow)}
        />
        <span className={styles.headerLabel}>{props.label}</span>
      </button>
      <Collapsible as="div" collapsed={collapsed} lazy={false}>
        <div className={styles.children}>{props.children}</div>
      </Collapsible>
    </div>
  );
}
```
</details>

- **Parameters**:
  - `props: ExpanderProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useCollapsible (from @docusaurus/theme-common)`
  - `clsx (from clsx)`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `ExpanderProps`

<details><summary>Interface Code</summary>

```ts
export interface ExpanderProps {
  readonly children?: React.ReactNode;
  readonly className?: string;
  readonly label: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `children` | `React.ReactNode` | ✓ |  |
| `className` | `string` | ✓ |  |
| `label` | `string` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---