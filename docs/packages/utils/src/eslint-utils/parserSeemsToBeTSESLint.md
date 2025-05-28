[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `parserSeemsToBeTSESLint.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
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