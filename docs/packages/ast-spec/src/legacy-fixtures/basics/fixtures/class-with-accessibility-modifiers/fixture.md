[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-with-accessibility-modifiers/fixture.ts`**

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