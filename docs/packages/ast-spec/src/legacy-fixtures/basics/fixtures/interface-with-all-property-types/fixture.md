[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/interface-with-all-property-types/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `Foo`

<details><summary>Interface Code</summary>

```ts
interface Foo {
  baa: number;
  bar?: number;
  [bax]: string;
  [baz]?: string;
  [eee: number]: string;
  doo(): void;
  coo?(a, b, c): void;
  [loo]?(a, b, c): void;
  boo<J>(a, b, c): void;
  new (a, b?): string;
  new <F>(a, b?): string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `baa` | `number` | ✗ |  |
| `bar` | `number` | ✓ |  |
| `[bax]` | `string` | ✗ |  |
| `[baz]` | `string` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---