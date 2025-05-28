[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `json.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 0 |
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
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/json.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `json5` | `json5` |
| `isRecord` | `../ast/utils` |


---

## Functions

### `ensureObject(obj: unknown): Record<string, unknown>`

<details><summary>Code</summary>

```ts
export function ensureObject(obj: unknown): Record<string, unknown> {
  return isRecord(obj) ? obj : {};
}
```
</details>

- **JSDoc**:
```ts
/**
 * Validates that the passed value is a record, if not return an empty object
 */
```

- **Parameters**:
  - `obj: unknown`
- **Return Type**: `Record<string, unknown>`
- **Calls**:
  - `isRecord (from ../ast/utils)`
### `parseJSONObject(code: string): Record<string, unknown>`

<details><summary>Code</summary>

```ts
export function parseJSONObject(code?: string): Record<string, unknown> {
  if (code) {
    try {
      return ensureObject(json5.parse(code));
    } catch (e) {
      console.error(e);
    }
  }
  return {};
}
```
</details>

- **JSDoc**:
```ts
/**
 * Parse a JSON string into an object. If the string is not valid JSON, return an empty object.
 */
```

- **Parameters**:
  - `code: string`
- **Return Type**: `Record<string, unknown>`
- **Calls**:
  - `ensureObject`
  - `json5.parse`
  - `console.error`
### `toJson(cfg: unknown): string`

<details><summary>Code</summary>

```ts
export function toJson(cfg: unknown): string {
  return JSON.stringify(cfg, null, 2);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Convert a config object to a JSON string
 */
```

- **Parameters**:
  - `cfg: unknown`
- **Return Type**: `string`
- **Calls**:
  - `JSON.stringify`
### `toJsonConfig(cfg: unknown, prop: string): string`

<details><summary>Code</summary>

```ts
export function toJsonConfig(cfg: unknown, prop: string): string {
  return toJson({ [prop]: cfg });
}
```
</details>

- **JSDoc**:
```ts
/**
 * Convert a config object to a JSON string, wrapping it in a property
 */
```

- **Parameters**:
  - `cfg: unknown`
  - `prop: string`
- **Return Type**: `string`
- **Calls**:
  - `toJson`

---