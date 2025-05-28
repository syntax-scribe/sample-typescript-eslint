[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `namespaced-attribute.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 2 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 3 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/jsx/namespaced-attribute.tsx`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `x` | `any` | const | `<Foo a:b="hello" />` | ✗ |
| `y` | `any` | const | `<Foo a:b="hello" />` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `Foo` | component | a:b="hello" | *none* |
| `Foo` | component | a:b="hello" | *none* |
| `div` | element | *none* | {props['a:b']} |


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