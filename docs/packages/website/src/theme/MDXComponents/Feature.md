[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Feature.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/theme/MDXComponents/Feature.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |
| `styles` | `./Feature.module.css` |


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

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---