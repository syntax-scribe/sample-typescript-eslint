[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `AlertBlock.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 1 |
| 💠 JSX Elements | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/layout/AlertBlock.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={`admonition alert alert--${props.type}`} | <div> |
| `div` | element | className="admonition-content" | {props.children} |


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