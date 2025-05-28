[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `EditorTabs.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
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
📂 **`packages/website/src/components/layout/EditorTabs.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `EditIcon` | `@site/src/icons/edit.svg` |
| `clsx` | `clsx` |
| `React` | `react` |
| `styles` | `./EditorTabs.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={clsx(styles.tabContainer, 'padding--xs')} | <div>, {showVisualEditor && (
        <button
          className={clsx(styles.tabStyle, 'button')}
          onClick={(): void => showModal?.(active)}
        >
          Visual Editor
          <EditIcon height={12} width={12} />
        </button>
      )} |
| `div` | element | className="button-group", role="tablist" | {tabsWithLabels.map(item => (
          <button
            aria-selected={active === item.value}
            className={clsx(styles.tabStyle, 'button')}
            disabled={active === item.value}
            key={item.label}
            onClick={(): void => change(item.value)}
            role="tab"
          >
            {item.label}
            {additionalTabsInfo?.[item.label] ? (
              <div className={styles.tabErrors}>
                {additionalTabsInfo[item.label] > 99
                  ? '99+'
                  : additionalTabsInfo[item.label]}
              </div>
            ) : null}
          </button>
        ))} |
| `button` | element | aria-selected={active === item.value}, className={clsx(styles.tabStyle, 'button')}, disabled={active === item.value}, key={item.label}, onClick={(): void => change(item.value)}, role="tab" | {item.label}, {additionalTabsInfo?.[item.label] ? (
              <div className={styles.tabErrors}>
                {additionalTabsInfo[item.label] > 99
                  ? '99+'
                  : additionalTabsInfo[item.label]}
              </div>
            ) : null} |
| `div` | element | className={styles.tabErrors} | {additionalTabsInfo[item.label] > 99
                  ? '99+'
                  : additionalTabsInfo[item.label]} |
| `button` | element | className={clsx(styles.tabStyle, 'button')}, onClick={(): void => showModal?.(active)} | text: "Visual Editor", <EditIcon> |
| `EditIcon` | component | height={12}, width={12} | *none* |


---

## Functions

### `EditorTabs({
  active,
  additionalTabsInfo,
  change,
  showModal,
  showVisualEditor,
  tabs,
}: EditorTabsProps<T>): React.JSX.Element`

<details><summary>Code</summary>

```ts
function EditorTabs<T extends boolean | string>({
  active,
  additionalTabsInfo,
  change,
  showModal,
  showVisualEditor,
  tabs,
}: EditorTabsProps<T>): React.JSX.Element {
  const tabsWithLabels = tabs.map(tab =>
    typeof tab !== 'object' ? { label: String(tab), value: tab } : tab,
  );

  return (
    <div className={clsx(styles.tabContainer, 'padding--xs')}>
      <div className="button-group" role="tablist">
        {tabsWithLabels.map(item => (
          <button
            aria-selected={active === item.value}
            className={clsx(styles.tabStyle, 'button')}
            disabled={active === item.value}
            key={item.label}
            onClick={(): void => change(item.value)}
            role="tab"
          >
            {item.label}
            {additionalTabsInfo?.[item.label] ? (
              <div className={styles.tabErrors}>
                {additionalTabsInfo[item.label] > 99
                  ? '99+'
                  : additionalTabsInfo[item.label]}
              </div>
            ) : null}
          </button>
        ))}
      </div>
      {showVisualEditor && (
        <button
          className={clsx(styles.tabStyle, 'button')}
          onClick={(): void => showModal?.(active)}
        >
          Visual Editor
          <EditIcon height={12} width={12} />
        </button>
      )}
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  active,
  additionalTabsInfo,
  change,
  showModal,
  showVisualEditor,
  tabs,
}: EditorTabsProps<T>`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `tabs.map`
  - `String`
  - `clsx (from clsx)`
  - `tabsWithLabels.map`
  - `change`
  - `showModal`

---

## Interfaces

### `EditorTabsProps<T extends boolean | string>`

<details><summary>Interface Code</summary>

```ts
export interface EditorTabsProps<T extends boolean | string> {
  readonly active: T;
  readonly additionalTabsInfo?: Record<string, number>;
  readonly change: (name: T) => void;
  readonly showModal?: (name: T) => void;
  readonly showVisualEditor?: boolean;
  readonly tabs: (T | { label: string; value: T })[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `active` | `T` | ✗ |  |
| `additionalTabsInfo` | `Record<string, number>` | ✓ |  |
| `change` | `(name: T) => void` | ✗ |  |
| `showModal` | `(name: T) => void` | ✓ |  |
| `showVisualEditor` | `boolean` | ✓ |  |
| `tabs` | `(T | { label: string; value: T })[]` | ✗ |  |


---