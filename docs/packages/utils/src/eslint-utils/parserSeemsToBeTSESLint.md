[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `parserSeemsToBeTSESLint.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/utils/src/eslint-utils/parserSeemsToBeTSESLint.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `parserSeemsToBeTSESLint(parser: string | undefined): boolean`

<details><summary>Code</summary>

```ts
export function parserSeemsToBeTSESLint(parser: string | undefined): boolean {
  return !!parser && /(?:typescript-eslint|\.\.)[\w/\\]*parser/.test(parser);
}
```
</details>

- **Parameters**:
  - `parser: string | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `/(?:typescript-eslint|\.\.)[\w/\\]*parser/.test`

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