[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📊 Variables & Constants | 2 |
| 💠 JSX Elements | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/jsx/JSXNamespacedName/fixtures/component-dashed/fixture.tsx`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `componentBasic` | `any` | const | `<foo />` | ✗ |
| `componentDashed` | `any` | const | `<foo-bar:baz-bam />` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `foo` | element | *none* | *none* |
| `foo-bar:baz-bam` | element | *none* | *none* |


---

## Interfaces

### `IntrinsicElements`

<details><summary>Interface Code</summary>

```ts
interface IntrinsicElements {
    foo: any;
    'foo-bar:baz-bam': any;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `foo` | `any` | ✗ |  |
| `'foo-bar:baz-bam'` | `any` | ✗ |  |


---