[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `recommended-type-checked-only.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/configs/flat/recommended-type-checked-only.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `FlatConfig` | `@typescript-eslint/utils/ts-eslint` |
| `baseConfig` | `./base` |
| `eslintRecommendedConfig` | `./eslint-recommended` |


---

## Functions

### `default_export_function(plugin: FlatConfig.Plugin, parser: FlatConfig.Parser): FlatConfig.ConfigArray`

<details><summary>Code</summary>

```ts
(
  plugin: FlatConfig.Plugin,
  parser: FlatConfig.Parser,
): FlatConfig.ConfigArray => [
  baseConfig(plugin, parser),
  eslintRecommendedConfig(plugin, parser),
  {
    name: 'typescript-eslint/recommended-type-checked-only',
    rules: {
      '@typescript-eslint/await-thenable': 'error',
      '@typescript-eslint/no-array-delete': 'error',
      '@typescript-eslint/no-base-to-string': 'error',
      '@typescript-eslint/no-duplicate-type-constituents': 'error',
      '@typescript-eslint/no-floating-promises': 'error',
      '@typescript-eslint/no-for-in-array': 'error',
      'no-implied-eval': 'off',
      '@typescript-eslint/no-implied-eval': 'error',
      '@typescript-eslint/no-misused-promises': 'error',
      '@typescript-eslint/no-redundant-type-constituents': 'error',
      '@typescript-eslint/no-unnecessary-type-assertion': 'error',
      '@typescript-eslint/no-unsafe-argument': 'error',
      '@typescript-eslint/no-unsafe-assignment': 'error',
      '@typescript-eslint/no-unsafe-call': 'error',
      '@typescript-eslint/no-unsafe-enum-comparison': 'error',
      '@typescript-eslint/no-unsafe-member-access': 'error',
      '@typescript-eslint/no-unsafe-return': 'error',
      '@typescript-eslint/no-unsafe-unary-minus': 'error',
      'no-throw-literal': 'off',
      '@typescript-eslint/only-throw-error': 'error',
      'prefer-promise-reject-errors': 'off',
      '@typescript-eslint/prefer-promise-reject-errors': 'error',
      'require-await': 'off',
      '@typescript-eslint/require-await': 'error',
      '@typescript-eslint/restrict-plus-operands': 'error',
      '@typescript-eslint/restrict-template-expressions': 'error',
      '@typescript-eslint/unbound-method': 'error',
    },
  },
]
```
</details>

- **Parameters**:
  - `plugin: FlatConfig.Plugin`
  - `parser: FlatConfig.Parser`
- **Return Type**: `FlatConfig.ConfigArray`

---