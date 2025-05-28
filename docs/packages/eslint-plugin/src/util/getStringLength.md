[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getStringLength.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
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

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getStringLength.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Graphemer` | `graphemer` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `splitter` | `Graphemer | undefined` | let/var | `*not shown*` | ✗ |


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