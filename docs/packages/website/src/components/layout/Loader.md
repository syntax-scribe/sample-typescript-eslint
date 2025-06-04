[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Loader.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |
| 💠 JSX Elements | 4 |

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