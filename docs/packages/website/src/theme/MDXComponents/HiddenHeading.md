[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `HiddenHeading.tsx`

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
📂 **`packages/website/src/theme/MDXComponents/HiddenHeading.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |
| `styles` | `./HiddenHeading.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `span` | element | className={styles.hiddenHeading}, id={id} | *none* |


---

## Functions

### `HiddenHeading({ id }: HiddenHeadingProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function HiddenHeading({ id }: HiddenHeadingProps): React.JSX.Element {
  return <span className={styles.hiddenHeading} id={id} />;
}
```
</details>

- **Parameters**:
  - `{ id }: HiddenHeadingProps`
- **Return Type**: `React.JSX.Element`

---

## Interfaces

### `HiddenHeadingProps`

<details><summary>Interface Code</summary>

```ts
export interface HiddenHeadingProps {
  id: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `id` | `string` | ✗ |  |


---