[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Feature.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |
| 💠 JSX Elements | 3 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/theme/MDXComponents/Feature.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |
| `styles` | `./Feature.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={styles.feature} | <div>, <p> |
| `div` | element | className={styles.emoji} | {emoji} |
| `p` | element | className={styles.children} | {children} |


---

## Functions

### `Feature({ children, emoji }: FeatureProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function Feature({ children, emoji }: FeatureProps): React.JSX.Element {
  return (
    <div className={styles.feature}>
      <div className={styles.emoji}>{emoji}</div>
      <p className={styles.children}>{children}</p>
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{ children, emoji }: FeatureProps`
- **Return Type**: `React.JSX.Element`

---

## Interfaces

### `FeatureProps`

<details><summary>Interface Code</summary>

```ts
export interface FeatureProps {
  children: React.ReactNode;
  emoji: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `children` | `React.ReactNode` | ✗ |  |
| `emoji` | `string` | ✗ |  |


---