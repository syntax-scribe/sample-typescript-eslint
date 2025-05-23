[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `string.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/util/serializers/string.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `NewPlugin` | `@vitest/pretty-format` |


---

## Functions

### `serialize(str: string): string`

<details><summary>Code</summary>

```ts
serialize(
    str: string,
    // config,
    // indentation,
    // depth,
    // refs,
    // printer,
  ) {
    return `'${str.replaceAll(/'|\\/g, '\\$&')}'`;
  }
```
</details>

- **Parameters**:
  - `str: string`
- **Return Type**: `string`
- **Calls**:
  - `str.replaceAll`
### `test(val: unknown): boolean`

<details><summary>Code</summary>

```ts
test(val: unknown) {
    return typeof val === 'string';
  }
```
</details>

- **Parameters**:
  - `val: unknown`
- **Return Type**: `boolean`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---