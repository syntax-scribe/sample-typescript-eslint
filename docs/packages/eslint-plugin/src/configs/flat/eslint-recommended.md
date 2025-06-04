[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `eslint-recommended.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/configs/flat/eslint-recommended.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `FlatConfig` | `@typescript-eslint/utils/ts-eslint` |
| `config` | `../eslint-recommended-raw` |


---

## Functions

### `default_export_function(_plugin: FlatConfig.Plugin, _parser: FlatConfig.Parser): FlatConfig.Config`

<details><summary>Code</summary>

```ts
(
  _plugin: FlatConfig.Plugin,
  _parser: FlatConfig.Parser,
): FlatConfig.Config => ({
  ...config('minimatch'),
  name: 'typescript-eslint/eslint-recommended',
})
```
</details>

- **Parameters**:
  - `_plugin: FlatConfig.Plugin`
  - `_parser: FlatConfig.Parser`
- **Return Type**: `FlatConfig.Config`

---