[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `escapeRegExp.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/escapeRegExp.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `reRegExpChar` | `RegExp` | const | `/[\\^$.*+?()[\]{}|]/g` | ✗ |


---

## Functions

### `escapeRegExp(string: string): string`

<details><summary>Code</summary>

```ts
export function escapeRegExp(string = ''): string {
  return string && reHasRegExpChar.test(string)
    ? string.replaceAll(reRegExpChar, '\\$&')
    : string;
}
```
</details>

- **Parameters**:
  - `string: string`
- **Return Type**: `string`
- **Calls**:
  - `reHasRegExpChar.test`
  - `string.replaceAll`

---