[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 1
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-with-accessibility-modifiers/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `Foo.getBar(): string`

<details><summary>Code</summary>

```ts
public getBar() {
    return this.bar;
  }
```
</details>

- **Return Type**: `string`
### `Foo.setBar(bar: string): void`

<details><summary>Code</summary>

```ts
protected setBar(bar: string) {
    this.bar = bar;
  }
```
</details>

- **Parameters**:
  - `bar: string`
- **Return Type**: `void`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  private bar: string;
  public static baz: number;
  public getBar() {
    return this.bar;
  }
  protected setBar(bar: string) {
    this.bar = bar;
  }
}
```
</details>

#### Methods

##### `getBar(): string`

<details><summary>Code</summary>

```ts
public getBar() {
    return this.bar;
  }
```
</details>

##### `setBar(bar: string): void`

<details><summary>Code</summary>

```ts
protected setBar(bar: string) {
    this.bar = bar;
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