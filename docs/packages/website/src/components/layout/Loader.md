[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Loader.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/layout/Loader.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `clsx` | `clsx` |
| `styles` | `./Loader.module.css` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---