[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `eslint-recommended.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
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