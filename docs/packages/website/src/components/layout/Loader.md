[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Loader.tsx`

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
| 💠 JSX Elements | 4 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/layout/Loader.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `clsx` | `clsx` |
| `styles` | `./Loader.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `span` | element | className={styles.loaderContainer} | <span>, <span>, <span> |
| `span` | element | className={clsx(styles.loader, styles.loader1)} | *none* |
| `span` | element | className={clsx(styles.loader, styles.loader2)} | *none* |
| `span` | element | className={clsx(styles.loader, styles.loader3)} | *none* |


---

## Functions

### `Loader(): React.JSX.Element`

<details><summary>Code</summary>

```ts
function Loader(): React.JSX.Element {
  return (
    <span className={styles.loaderContainer}>
      <span className={clsx(styles.loader, styles.loader1)} />
      <span className={clsx(styles.loader, styles.loader2)} />
      <span className={clsx(styles.loader, styles.loader3)} />
    </span>
  );
}
```
</details>

- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `clsx (from clsx)`

---