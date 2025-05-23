[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getStringLength.ts`

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
📂 **`packages/eslint-plugin/src/util/getStringLength.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Graphemer` | `graphemer` |


---

## Functions

### `isASCII(value: string): boolean`

<details><summary>Code</summary>

```ts
function isASCII(value: string): boolean {
  return /^[\u0020-\u007f]*$/u.test(value);
}
```
</details>

- **Parameters**:
  - `value: string`
- **Return Type**: `boolean`
- **Calls**:
  - `/^[\u0020-\u007f]*$/u.test`
### `getStringLength(value: string): number`

<details><summary>Code</summary>

```ts
export function getStringLength(value: string): number {
  if (isASCII(value)) {
    return value.length;
  }

  splitter ??= new Graphemer();

  return splitter.countGraphemes(value);
}
```
</details>

- **Parameters**:
  - `value: string`
- **Return Type**: `number`
- **Calls**:
  - `isASCII`
  - `splitter.countGraphemes`

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