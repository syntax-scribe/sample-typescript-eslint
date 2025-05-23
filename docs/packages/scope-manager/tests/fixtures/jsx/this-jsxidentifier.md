[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `this-jsxidentifier.tsx`

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 1
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/jsx/this-jsxidentifier.tsx`**

## 📦 Imports

> No imports found in this file.


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

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---