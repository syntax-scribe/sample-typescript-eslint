[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `noFormat.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-tester/src/noFormat.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `noFormat(raw: TemplateStringsArray, keys: string[]): string`

<details><summary>Code</summary>

```ts
export function noFormat(raw: TemplateStringsArray, ...keys: string[]): string {
  return String.raw({ raw }, ...keys);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Simple no-op tag to mark code samples as "should not format with prettier"
 *   for the plugin-test-formatting lint rule
 */
```

- **Parameters**:
  - `raw: TemplateStringsArray`
  - `keys: string[]`
- **Return Type**: `string`
- **Calls**:
  - `String.raw`

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