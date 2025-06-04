[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `ignore-type-only-stuff.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📊 Variables & Constants | 1 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/ignore-type-only-stuff.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `a` | `C` | let/var | `*not shown*` | ✗ |


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