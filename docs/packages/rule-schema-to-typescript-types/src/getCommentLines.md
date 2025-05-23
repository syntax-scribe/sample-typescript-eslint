[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getCommentLines.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-schema-to-typescript-types/src/getCommentLines.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---