[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `escapeRegExp.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

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