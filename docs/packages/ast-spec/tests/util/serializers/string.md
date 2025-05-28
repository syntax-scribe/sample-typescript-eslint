[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `string.ts`

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
📂 **`packages/ast-spec/tests/util/serializers/string.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `NewPlugin` | `@vitest/pretty-format` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `serializer` | `NewPlugin` | const | `{
  serialize(
    str: string,
    // config,
    // indentation,
    // depth,
    // refs,
    // printer,
  ) {
    return `'${str.replaceAll(/'|\\/g, '\\$&')}'`;
  },
  test(val: unknown) {
    return typeof val === 'string';
  },
}` | ✓ |


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