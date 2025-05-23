[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `eslint-recommended.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---