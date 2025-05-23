[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `HiddenHeading.tsx`

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
📂 **`packages/website/src/theme/MDXComponents/HiddenHeading.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |
| `styles` | `./HiddenHeading.module.css` |


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

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---