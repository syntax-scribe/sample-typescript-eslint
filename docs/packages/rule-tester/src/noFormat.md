[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `noFormat.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/noFormat.ts`**

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