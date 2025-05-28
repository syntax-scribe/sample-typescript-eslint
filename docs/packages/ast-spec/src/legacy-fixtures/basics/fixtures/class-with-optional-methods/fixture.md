[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 1 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-with-optional-methods/fixture.ts`**

## Functions

### `Foo.foo(): any`

<details><summary>Code</summary>

```ts
foo?();
```
</details>

- **Return Type**: `any`
### `Foo.bar(): string`

<details><summary>Code</summary>

```ts
bar?(): string;
```
</details>

- **Return Type**: `string`
### `Foo.baz(): string`

<details><summary>Code</summary>

```ts
private baz?(): string;
```
</details>

- **Return Type**: `string`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  foo?();
  bar?(): string;
  private baz?(): string;
}
```
</details>

#### Methods

##### `foo(): any`

<details><summary>Code</summary>

```ts
foo?();
```
</details>

##### `bar(): string`

<details><summary>Code</summary>

```ts
bar?(): string;
```
</details>

##### `baz(): string`

<details><summary>Code</summary>

```ts
private baz?(): string;
```
</details>


---