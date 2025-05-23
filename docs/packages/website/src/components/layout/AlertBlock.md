[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `AlertBlock.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/layout/AlertBlock.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |


---

## Functions

### `AlertBlock(props: AlertBlockProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function AlertBlock(props: AlertBlockProps): React.JSX.Element {
  return (
    <div className={`admonition alert alert--${props.type}`}>
      <div className="admonition-content">{props.children}</div>
    </div>
  );
}
```
</details>

- **Parameters**:
  - `props: AlertBlockProps`
- **Return Type**: `React.JSX.Element`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `AlertBlockProps`

<details><summary>Interface Code</summary>

```ts
export interface AlertBlockProps {
  readonly children: React.ReactNode;
  readonly type: 'danger' | 'info' | 'note' | 'success' | 'warning';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `children` | `React.ReactNode` | ✗ |  |
| `type` | `'danger' | 'info' | 'note' | 'success' | 'warning'` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---