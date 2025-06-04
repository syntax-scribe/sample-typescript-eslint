[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `strict.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/configs/flat/strict.ts`**

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
    name: 'typescript-eslint/strict',
    rules: {
      '@typescript-eslint/ban-ts-comment': [
        'error',
        { minimumDescriptionLength: 10 },
      ],
      'no-array-constructor': 'off',
      '@typescript-eslint/no-array-constructor': 'error',
      '@typescript-eslint/no-duplicate-enum-values': 'error',
      '@typescript-eslint/no-dynamic-delete': 'error',
      '@typescript-eslint/no-empty-object-type': 'error',
      '@typescript-eslint/no-explicit-any': 'error',
      '@typescript-eslint/no-extra-non-null-assertion': 'error',
      '@typescript-eslint/no-extraneous-class': 'error',
      '@typescript-eslint/no-invalid-void-type': 'error',
      '@typescript-eslint/no-misused-new': 'error',
      '@typescript-eslint/no-namespace': 'error',
      '@typescript-eslint/no-non-null-asserted-nullish-coalescing': 'error',
      '@typescript-eslint/no-non-null-asserted-optional-chain': 'error',
      '@typescript-eslint/no-non-null-assertion': 'error',
      '@typescript-eslint/no-require-imports': 'error',
      '@typescript-eslint/no-this-alias': 'error',
      '@typescript-eslint/no-unnecessary-type-constraint': 'error',
      '@typescript-eslint/no-unsafe-declaration-merging': 'error',
      '@typescript-eslint/no-unsafe-function-type': 'error',
      'no-unused-expressions': 'off',
      '@typescript-eslint/no-unused-expressions': 'error',
      'no-unused-vars': 'off',
      '@typescript-eslint/no-unused-vars': 'error',
      'no-useless-constructor': 'off',
      '@typescript-eslint/no-useless-constructor': 'error',
      '@typescript-eslint/no-wrapper-object-types': 'error',
      '@typescript-eslint/prefer-as-const': 'error',
      '@typescript-eslint/prefer-literal-enum-member': 'error',
      '@typescript-eslint/prefer-namespace-keyword': 'error',
      '@typescript-eslint/triple-slash-reference': 'error',
      '@typescript-eslint/unified-signatures': 'error',
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