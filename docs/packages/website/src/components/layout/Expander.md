[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Expander.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 6 |
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

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={clsx(styles.expander, props.className)} | <button>, <Collapsible> |
| `button` | element | className={styles.heading}, onClick={toggleCollapsed} | <ArrowIcon>, <span> |
| `ArrowIcon` | component | className={clsx(styles.arrow, !collapsed && styles.expandedArrow)} | *none* |
| `span` | element | className={styles.headerLabel} | {props.label} |
| `Collapsible` | component | as="div", collapsed={collapsed}, lazy={false} | <div> |
| `div` | element | className={styles.children} | {props.children} |


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