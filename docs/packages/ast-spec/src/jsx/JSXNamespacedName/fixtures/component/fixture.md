[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.tsx`

## 📚 Table of Contents

- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/jsx/JSXNamespacedName/fixtures/component/fixture.tsx`**

## 📦 Imports

> No imports found in this file.


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

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---