[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `raw-plugin.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 30 |
| 📊 Variables & Constants | 4 |
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
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/raw-plugin.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `FlatConfig` | `@typescript-eslint/utils/ts-eslint` |
| `Linter` | `@typescript-eslint/utils/ts-eslint` |
| `all` | `./configs/eslintrc/all` |
| `base` | `./configs/eslintrc/base` |
| `disableTypeChecked` | `./configs/eslintrc/disable-type-checked` |
| `eslintRecommended` | `./configs/eslintrc/eslint-recommended` |
| `recommended` | `./configs/eslintrc/recommended` |
| `recommendedTypeChecked` | `./configs/eslintrc/recommended-type-checked` |
| `recommendedTypeCheckedOnly` | `./configs/eslintrc/recommended-type-checked-only` |
| `strict` | `./configs/eslintrc/strict` |
| `strictTypeChecked` | `./configs/eslintrc/strict-type-checked` |
| `strictTypeCheckedOnly` | `./configs/eslintrc/strict-type-checked-only` |
| `stylistic` | `./configs/eslintrc/stylistic` |
| `stylisticTypeChecked` | `./configs/eslintrc/stylistic-type-checked` |
| `stylisticTypeCheckedOnly` | `./configs/eslintrc/stylistic-type-checked-only` |
| `allFlat` | `./configs/flat/all` |
| `baseFlat` | `./configs/flat/base` |
| `disableTypeCheckedFlat` | `./configs/flat/disable-type-checked` |
| `eslintRecommendedFlat` | `./configs/flat/eslint-recommended` |
| `recommendedFlat` | `./configs/flat/recommended` |
| `recommendedTypeCheckedFlat` | `./configs/flat/recommended-type-checked` |
| `recommendedTypeCheckedOnlyFlat` | `./configs/flat/recommended-type-checked-only` |
| `strictFlat` | `./configs/flat/strict` |
| `strictTypeCheckedFlat` | `./configs/flat/strict-type-checked` |
| `strictTypeCheckedOnlyFlat` | `./configs/flat/strict-type-checked-only` |
| `stylisticFlat` | `./configs/flat/stylistic` |
| `stylisticTypeCheckedFlat` | `./configs/flat/stylistic-type-checked` |
| `stylisticTypeCheckedOnlyFlat` | `./configs/flat/stylistic-type-checked-only` |
| `rules` | `./rules` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `parser` | `TSESLint.FlatConfig.Parser` | const | `{
  meta: parserBase.meta,
  parseForESLint: parserBase.parseForESLint,
}` | ✗ |
| `plugin` | `Linter.Plugin` | const | `{
  // not fully initialized yet.
  // See https://eslint.org/docs/latest/extend/plugins#configs-in-plugins
  configs: {
    all,
    base,
    'disable-type-checked': disableTypeChecked,
    'eslint-recommended': eslintRecommended,
    recommended,
    /** @deprecated - please use "recommended-type-checked" instead. */
    'recommended-requiring-type-checking': recommendedTypeChecked,
    'recommended-type-checked': recommendedTypeChecked,
    'recommended-type-checked-only': recommendedTypeCheckedOnly,
    strict,
    'strict-type-checked': strictTypeChecked,
    'strict-type-checked-only': strictTypeCheckedOnly,
    stylistic,
    'stylistic-type-checked': stylisticTypeChecked,
    'stylistic-type-checked-only': stylisticTypeCheckedOnly,
  },
  meta: {
    name,
    version,
  },
  rules,
} satisfies Linter.Plugin` | ✗ |
| `flatPlugin` | `FlatConfig.Plugin` | const | `plugin as FlatConfig.Plugin` | ✗ |
| `flatConfigs` | `{ 'flat/all': FlatConfig.ConfigArray; 'flat/base': FlatConfig.Config; 'flat/disable-type-checked': FlatConfig.Config; 'flat/eslint-recommended': FlatConfig.Config; 'flat/recommended': FlatConfig.ConfigArray; 'flat/recommended-type-checked': FlatConfig.ConfigArray; 'flat/recommended-type-checked-only': FlatConfig.Con...` | const | `{
  'flat/all': allFlat(flatPlugin, parser),
  'flat/base': baseFlat(flatPlugin, parser),
  'flat/disable-type-checked': disableTypeCheckedFlat(flatPlugin, parser),
  'flat/eslint-recommended': eslintRecommendedFlat(flatPlugin, parser),
  'flat/recommended': recommendedFlat(flatPlugin, parser),
  'flat/recommended-type-checked': recommendedTypeCheckedFlat(
    flatPlugin,
    parser,
  ),
  'flat/recommended-type-checked-only': recommendedTypeCheckedOnlyFlat(
    flatPlugin,
    parser,
  ),
  'flat/strict': strictFlat(flatPlugin, parser),
  'flat/strict-type-checked': strictTypeCheckedFlat(flatPlugin, parser),
  'flat/strict-type-checked-only': strictTypeCheckedOnlyFlat(
    flatPlugin,
    parser,
  ),
  'flat/stylistic': stylisticFlat(flatPlugin, parser),
  'flat/stylistic-type-checked': stylisticTypeCheckedFlat(flatPlugin, parser),
  'flat/stylistic-type-checked-only': stylisticTypeCheckedOnlyFlat(
    flatPlugin,
    parser,
  ),
} satisfies Record<
  `flat/${string}`,
  TSESLint.FlatConfig.Config | TSESLint.FlatConfig.ConfigArray
>` | ✗ |


---


---