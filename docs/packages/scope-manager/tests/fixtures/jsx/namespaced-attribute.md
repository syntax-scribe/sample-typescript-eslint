[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `namespaced-attribute.tsx`

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
📂 **`packages/scope-manager/tests/fixtures/jsx/namespaced-attribute.tsx`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `Foo(props: FooProps): any`

<details><summary>Code</summary>

```ts
function Foo(props: FooProps) {
  return <div>{props['a:b']}</div>;
}
```
</details>

- **Parameters**:
  - `props: FooProps`
- **Return Type**: `any`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `FooProps`

<details><summary>Interface Code</summary>

```ts
interface FooProps {
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