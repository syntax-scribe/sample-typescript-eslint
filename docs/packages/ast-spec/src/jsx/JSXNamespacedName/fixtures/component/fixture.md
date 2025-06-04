[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 2 |
| 💠 JSX Elements | 3 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/jsx/JSXNamespacedName/fixtures/component/fixture.tsx`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `x` | `any` | const | `<NamespacePropComponent a:b="tight spacing" />` | ✗ |
| `y` | `any` | const | `<NamespacePropComponent a:b="loose spacing" />` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `NamespacePropComponent` | component | a:b="tight spacing" | *none* |
| `NamespacePropComponent` | component | a:b="loose spacing" | *none* |
| `div` | element | *none* | {props['a:b']} |


---

## Functions

### `NamespacePropComponent(props: NamespacePropComponentProps): any`

<details><summary>Code</summary>

```ts
function NamespacePropComponent(props: NamespacePropComponentProps) {
  return <div>{props['a:b']}</div>;
}
```
</details>

- **Parameters**:
  - `props: NamespacePropComponentProps`
- **Return Type**: `any`

---

## Interfaces

### `NamespacePropComponentProps`

<details><summary>Interface Code</summary>

```ts
interface NamespacePropComponentProps {
  'a:b': string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `'a:b'` | `string` | ✗ |  |


---