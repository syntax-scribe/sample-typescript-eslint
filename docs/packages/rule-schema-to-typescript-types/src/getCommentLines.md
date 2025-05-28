[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getCommentLines.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
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
📂 **`packages/rule-schema-to-typescript-types/src/getCommentLines.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `lines` | `string[]` | const | `[]` | ✗ |


---

## Functions

### `getCommentLines(schema: JSONSchema4): string[]`

<details><summary>Code</summary>

```ts
export function getCommentLines(schema: JSONSchema4): string[] {
  const lines: string[] = [];
  if (schema.description) {
    lines.push(schema.description);
  }
  return lines;
}
```
</details>

- **Parameters**:
  - `schema: JSONSchema4`
- **Return Type**: `string[]`
- **Calls**:
  - `lines.push`

---