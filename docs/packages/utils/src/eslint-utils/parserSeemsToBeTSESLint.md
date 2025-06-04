[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `parserSeemsToBeTSESLint.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/utils/src/eslint-utils/parserSeemsToBeTSESLint.ts`**

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