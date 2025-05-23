[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `disable-type-checked.ts`

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
📂 **`packages/eslint-plugin/src/configs/flat/disable-type-checked.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `FlatConfig` | `@typescript-eslint/utils/ts-eslint` |


---

## Functions

### `default_export_function(_plugin: FlatConfig.Plugin, _parser: FlatConfig.Parser): FlatConfig.Config`

<details><summary>Code</summary>

```ts
(
  _plugin: FlatConfig.Plugin,
  _parser: FlatConfig.Parser,
): FlatConfig.Config => ({
  name: 'typescript-eslint/disable-type-checked',
  rules: {
    '@typescript-eslint/await-thenable': 'off',
    '@typescript-eslint/consistent-return': 'off',
    '@typescript-eslint/consistent-type-exports': 'off',
    '@typescript-eslint/dot-notation': 'off',
    '@typescript-eslint/naming-convention': 'off',
    '@typescript-eslint/no-array-delete': 'off',
    '@typescript-eslint/no-base-to-string': 'off',
    '@typescript-eslint/no-confusing-void-expression': 'off',
    '@typescript-eslint/no-deprecated': 'off',
    '@typescript-eslint/no-duplicate-type-constituents': 'off',
    '@typescript-eslint/no-floating-promises': 'off',
    '@typescript-eslint/no-for-in-array': 'off',
    '@typescript-eslint/no-implied-eval': 'off',
    '@typescript-eslint/no-meaningless-void-operator': 'off',
    '@typescript-eslint/no-misused-promises': 'off',
    '@typescript-eslint/no-misused-spread': 'off',
    '@typescript-eslint/no-mixed-enums': 'off',
    '@typescript-eslint/no-redundant-type-constituents': 'off',
    '@typescript-eslint/no-unnecessary-boolean-literal-compare': 'off',
    '@typescript-eslint/no-unnecessary-condition': 'off',
    '@typescript-eslint/no-unnecessary-qualifier': 'off',
    '@typescript-eslint/no-unnecessary-template-expression': 'off',
    '@typescript-eslint/no-unnecessary-type-arguments': 'off',
    '@typescript-eslint/no-unnecessary-type-assertion': 'off',
    '@typescript-eslint/no-unnecessary-type-conversion': 'off',
    '@typescript-eslint/no-unnecessary-type-parameters': 'off',
    '@typescript-eslint/no-unsafe-argument': 'off',
    '@typescript-eslint/no-unsafe-assignment': 'off',
    '@typescript-eslint/no-unsafe-call': 'off',
    '@typescript-eslint/no-unsafe-enum-comparison': 'off',
    '@typescript-eslint/no-unsafe-member-access': 'off',
    '@typescript-eslint/no-unsafe-return': 'off',
    '@typescript-eslint/no-unsafe-type-assertion': 'off',
    '@typescript-eslint/no-unsafe-unary-minus': 'off',
    '@typescript-eslint/non-nullable-type-assertion-style': 'off',
    '@typescript-eslint/only-throw-error': 'off',
    '@typescript-eslint/prefer-destructuring': 'off',
    '@typescript-eslint/prefer-find': 'off',
    '@typescript-eslint/prefer-includes': 'off',
    '@typescript-eslint/prefer-nullish-coalescing': 'off',
    '@typescript-eslint/prefer-optional-chain': 'off',
    '@typescript-eslint/prefer-promise-reject-errors': 'off',
    '@typescript-eslint/prefer-readonly': 'off',
    '@typescript-eslint/prefer-readonly-parameter-types': 'off',
    '@typescript-eslint/prefer-reduce-type-parameter': 'off',
    '@typescript-eslint/prefer-regexp-exec': 'off',
    '@typescript-eslint/prefer-return-this-type': 'off',
    '@typescript-eslint/prefer-string-starts-ends-with': 'off',
    '@typescript-eslint/promise-function-async': 'off',
    '@typescript-eslint/related-getter-setter-pairs': 'off',
    '@typescript-eslint/require-array-sort-compare': 'off',
    '@typescript-eslint/require-await': 'off',
    '@typescript-eslint/restrict-plus-operands': 'off',
    '@typescript-eslint/restrict-template-expressions': 'off',
    '@typescript-eslint/return-await': 'off',
    '@typescript-eslint/strict-boolean-expressions': 'off',
    '@typescript-eslint/switch-exhaustiveness-check': 'off',
    '@typescript-eslint/unbound-method': 'off',
    '@typescript-eslint/use-unknown-in-catch-callback-variable': 'off',
  },
  languageOptions: {
    parserOptions: { program: null, project: false, projectService: false },
  },
})
```
</details>

- **Parameters**:
  - `_plugin: FlatConfig.Plugin`
  - `_parser: FlatConfig.Parser`
- **Return Type**: `FlatConfig.Config`

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