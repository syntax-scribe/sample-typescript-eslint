[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `ignore-type-only-stuff.ts`

## 📚 Table of Contents

- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 2
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/ignore-type-only-stuff.ts`**

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

### `B`

<details><summary>Interface Code</summary>

```ts
interface B {
  prop1: A;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `prop1` | `A` | ✗ |  |

### `C`

<details><summary>Interface Code</summary>

```ts
interface C extends B {
  method(a: { b: A }): { c: A };
}
```
</details>


---

## Type Aliases

### `A`

```ts
type A = number;
```


---