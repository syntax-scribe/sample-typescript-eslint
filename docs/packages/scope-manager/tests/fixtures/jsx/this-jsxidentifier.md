[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `this-jsxidentifier.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 1 |
| 📊 Variables & Constants | 1 |
| 💠 JSX Elements | 4 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/jsx/this-jsxidentifier.tsx`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `React` | `any` | let/var | `*not shown*` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | *none* | *none* |
| `this.foo` | element | *none* | *none* |
| `Div.Element` | component | *none* | *none* |
| `this` | element | *none* | *none* |


---

## Functions

### `Foo.method(): void`

<details><summary>Code</summary>

```ts
method() {
    <this.foo />;
    (<Div.Element />)(<this />);
  }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `complex_call_124`
### `Element(): any`

<details><summary>Code</summary>

```ts
() => <div />
```
</details>

- **Return Type**: `any`
### `Element(): any`

<details><summary>Code</summary>

```ts
() => <div />
```
</details>

- **Return Type**: `any`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  foo: any;
  Div = {
    Element: () => <div />,
  };
  method() {
    <this.foo />;
    (<Div.Element />)(<this />);
  }
}
```
</details>

#### Methods

##### `method(): void`

<details><summary>Code</summary>

```ts
method() {
    <this.foo />;
    (<Div.Element />)(<this />);
  }
```
</details>


---