[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `base.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/configs/flat/base.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `FlatConfig` | `@typescript-eslint/utils/ts-eslint` |


---

## Functions

### `default_export_function(plugin: FlatConfig.Plugin, parser: FlatConfig.Parser): FlatConfig.Config`

<details><summary>Code</summary>

```ts
(
  plugin: FlatConfig.Plugin,
  parser: FlatConfig.Parser,
): FlatConfig.Config => ({
  name: 'typescript-eslint/base',
  languageOptions: {
    parser,
    sourceType: 'module',
  },
  plugins: {
    '@typescript-eslint': plugin,
  },
})
```
</details>

- **Parameters**:
  - `plugin: FlatConfig.Plugin`
  - `parser: FlatConfig.Parser`
- **Return Type**: `FlatConfig.Config`

---