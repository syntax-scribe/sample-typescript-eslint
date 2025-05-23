[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `base.ts`

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---